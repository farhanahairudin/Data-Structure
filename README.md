# Data-Structure
import java.util.*;/**
 *
 * @author Farhana
 */
public class QueueSystem {

    /**
     * @param args the command line arguments
     */
    
   private static Queue<Integer> normal = new LinkedList<Integer>();
         
   private static Queue<Integer> vip = new LinkedList<Integer>();

   private static int time = 1440;

   private static int longestWait = 0;

   private static int[] service = {0, 0, 0};

   private static int custService = 0;

   private static int totalWait = 0;

   private static int vipWait = 0;

   private static int vipCust = 0;

   private static int vipLongestWait = 0;
   
   public static void main(String[] args) {
        
       for(int x = 1; x <= time; x++) {

         if(Math.random() < .5) {

            if(normal.size() < service.length)

               for(int k = 0; k < service.length; k++)

                  if(service[k] == 0)

                  {

                     service[k] = (int)(Math.random() * 6 + 2);

                     break;

                  }

            normal.add(x);      

         }

         if(Math.random() < .05) {

            if(vip.size() < service.length)

               for(int k = 0; k < service.length; k++)

                  if(service[k] == 0)

                  {

                     service[k] = (int)(Math.random() * 6 + 2);

                     break;

                  }

            vip.add(x);     

         }

         if(!vip.isEmpty()) {

            vipServe(vip, x);

         System.out.print("VIP Customer(s): ");

            printQueue(vip);

         }

         else {

            normalServe(normal, x);

         System.out.print("Normal Customer(s): ");

          

            printQueue(normal);

         }

      }

      System.out.println("\n" + "*****Normal Customers*****");

      System.out.println("Total number of customers: " + custService);

      System.out.println("Average Wait Time: " + (double)totalWait/custService);

      System.out.println("Longest Wait Time: " + longestWait);

       

      System.out.println();

      System.out.println("*****VIP Customers*****" + "\n");

      System.out.println("Total number of customers: " + vipCust);

      System.out.println("Average Wait Time: " + (double)vipWait/vipCust);

      System.out.println("Longest Wait Time: " + vipLongestWait);

    

   }
    //method for normal customers queue
    
    public static void normalServe(Queue<Integer> normal, int x)

   {

      for(int y = 0; y < service.length; y++)

      {

         if(service[y] > 0)

            service[y]--;

         else if(normal.size() > 3) {

            if(x - normal.peek() > longestWait)

               longestWait = x - normal.peek();

            totalWait += x - normal.remove();

            custService++;

            service[y] = (int)(Math.random() * 6 + 2); 

         }

         else if(!normal.isEmpty() ) {

            if(x - normal.peek() > longestWait)

               longestWait = x - normal.peek();

            totalWait += x - normal.remove();

            custService++;

         }

      }

   }
    //method for vip customers queue
    
    public static void vipServe(Queue<Integer> normal, int x)

   {

      for(int y = 0; y < service.length; y++)

      {

         if(service[y] > 0)

            service[y]--;

         else if(normal.size() > 3) {

            if(x - normal.peek() > vipLongestWait)

               vipLongestWait = x - normal.peek();

            vipWait += x - normal.remove();

            vipCust++;

            service[y] = (int)(Math.random() * 6 + 2); 

         }

         else if(!normal.isEmpty() ) {

            if(x - normal.peek() > vipLongestWait)

               vipLongestWait = x - normal.peek();

            vipWait += x - normal.remove();

            vipCust++;

         }

      }

   }

    public static void printQueue(Queue<Integer> yo) {
       
        System.out.println(yo.toString());
        
    }
    
}
