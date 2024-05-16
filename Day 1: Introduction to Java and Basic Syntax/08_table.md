```

public class table {
	void print(int table ,int f,int r)
	{
		for(int i=f;i<r;i++)
		{
			System.out.printf("%d * %d = %d ",table,i,table*i).println();
			
		}
	}
	}

public class mrun {

	public static void main(String[] args) {
     table t1=new table();
     t1.print(3,10,20);  
	}
}

#OUTPUT

3 * 10 = 30 
3 * 11 = 33 
3 * 12 = 36 
3 * 13 = 39 
3 * 14 = 42 
3 * 15 = 45 
3 * 16 = 48 
3 * 17 = 51 
3 * 18 = 54 
3 * 19 = 57
```
