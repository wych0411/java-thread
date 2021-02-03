# simple thread code style

## simple thread extends Thread

    public class TimeCoster extends Thread {

      public void run(){
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(String.format(">>Thread %s complete!", this.getName()));
      }
    }
