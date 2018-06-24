# log4j 异步记录log类解析--AsyncAppender
```
//存储在buffer中logevent的数量限制
public static final int DEFAULT_BUFFER_SIZE = 128;
//底层使用一个arraylist来对logevent进行缓存
private final List buffer = new ArrayList();
//使用一个hashmap对需要排除的logevent进行缓存
private final Map discardMap = new HashMap();
//异步的线程进行log的记录
  private final Thread dispatcher;
//是否显示log中的location信息
  private boolean locationInfo = false;
//当缓存的个数超过最大个数时是否进行阻塞线程
  private boolean blocking = true;
//构造方法，此方法进行异步线程的初始化，确保线程之启动一次
  public AsyncAppender() {
    appenders = new AppenderAttachableImpl();
    aai = appenders;

    dispatcher =
      new Thread(new Dispatcher(this, buffer, discardMap, appenders));

    // It is the user's responsibility to close appenders before
    // exiting.
    dispatcher.setDaemon(true);

    // set the dispatcher priority to lowest possible value
    //        dispatcher.setPriority(Thread.MIN_PRIORITY);
    dispatcher.setName("AsyncAppender-Dispatcher-" + dispatcher.getName());
    dispatcher.start();
  }
  //核心方法
  public void append(final LoggingEvent event) {
    //当异步的自线程被干掉之后，采用同步的方式进行log的记录
    if ((dispatcher == null) || !dispatcher.isAlive() || (bufferSize <= 0)) {
      synchronized (appenders) {
        appenders.appendLoopOnAppenders(event);
      }
      return;
    }

    //这部分的内容好像是要确认event中的内容是否完整
    event.getNDC();
    event.getThreadName();
    // Get a copy of this thread's MDC.
    event.getMDCCopy();
    if (locationInfo) {
      event.getLocationInformation();
    }
    event.getRenderedMessage();
    event.getThrowableStrRep();

    //将buffer锁住之后进行buffer中内容的添加，保证线程的同步性
    synchronized (buffer) {
      //通过一个循环来当buffer个数达到上限时如何操作
      while (true) {
        int previousSize = buffer.size();
        //当还没有达到上限时直接添加到buffer中然后释放锁
        if (previousSize < bufferSize) {
          buffer.add(event);
          //如果buffer中的个数为0，需要notify其他线程进行操作
          if (previousSize == 0) {
            buffer.notifyAll();
          }
          break;
        }

        boolean discard = true;
        if (blocking
                && !Thread.interrupted()
                && Thread.currentThread() != dispatcher) {
          try {
            buffer.wait();
            discard = false;
          } catch (InterruptedException e) {
            //
            //  reset interrupt status so
            //    calling code can see interrupt on
            //    their next wait or sleep.
            Thread.currentThread().interrupt();
          }
        }

        //
        //   如果用户选择不进行堵塞，就讲代码放到hashmap中进行缓存
        //
        if (discard) {
          String loggerName = event.getLoggerName();
          DiscardSummary summary = (DiscardSummary) discardMap.get(loggerName);

          if (summary == null) {
            summary = new DiscardSummary(event);
            discardMap.put(loggerName, summary);
          } else {
            summary.add(event);
          }

          break;
        }
      }
    }
  }

