```
public class TriangleValidator {
    public boolean isValidTriangle(int angle1, int angle2, int angle3) {
        // write your code here
        if((angle1>0)&&(angle2>0)&&(angle3>0))
        {
            int sum=angle1+angle2+angle3;
            if(sum==180){
             System.out.println("This is a valid traingle");
             }
            else 
             return false;
            return true;
            
            
        }
        else
        {
            return false;
        }
        
    }
}
```
