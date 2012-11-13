# wget

wget java download library.

support single thread, single thread with download continue / resume, and multithread download.

## Exceptions

Here is a three kind of exceptions.

1) Fatal exception. all RuntimeException's
  We shall stop application

2) DownloadError (extends RuntimeException)
  We unable to process following url and shall stop to download it
  
3) DownloadRetry (caused by IOException)
  We're having temporary problems. Shall retry download after a delay.

## Example

        // simple example. direct one call download

        try {
            WGet w = new WGet(new URL("http://www.dd-wrt.com/routerdb/de/download/D-Link/DIR-300/A1/ap61.ram/2049"),
                    new File("/Users/axet/Downloads/"));
            // will block until download finishes
            w.download();
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }

## Example multithread

    public static void main(String[] args) {
        try {
            AtomicBoolean stop = new AtomicBoolean(false);
            Runnable notify = new Runnable() {

                @Override
                public void run() {
                    // notify app or save download state
                }
            };
            DownloadInfo info = new DownloadInfo(new URL(
                    "http://download.virtualbox.org/virtualbox/4.2.4/VirtualBox-4.2.4-81684-OSX.dmg"));
            info.extract();
            info.enableMultipart();
            WGet w = new WGet(info, new File("/Users/axet/Downloads/VirtualBox-4.2.4-81684-OSX.dmg"), stop, notify);
            w.download();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }

## More examples

Go to the examples source folder.