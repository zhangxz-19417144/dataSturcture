####  数组的基本操作

###### 1.创建数组

```java
public class Main {

    public static void main(String[] args) {
	// 第一种创建数组的方式
        int[] arr=new int[20];

        for(int i=0;i<arr.length;i++) {
            arr[i]=i;
           System.out.println(arr[i]);
        }

   // 第二种创建数组的方式
        int[] scores=new int[]{100,99,98};
        for(int score:scores){
            System.out.println(score);
        }
    }
}
```

###### 2.创建数组的构造方法和其他的基本方法

```java
public class Array {
    private int[] data;
    //实际上有几个元素，capacity是容量：就是最多可以装多少个元素，没有capacity是因为.length可以代替
    //size的位置也是第一个没有存放元素的索引，eg：数组没有元素size=0，第一个没有存放元素的索引是0，数组一个元素size=1，第一个没有存放元素的索引是1.
    private int size;

    //有参构造函数，用户可以根据需要设置容量
    public Array(int capacity){
        data=new int[capacity];
        size=0;
    }

    //无参构造函数，用户调用这个构造函数的时候默认的容量是10
    public Array(){
        this(10);
    }

    //获取数组中的元素个数
    public int getSize(){
        return size;
    }

    //获取数组的容量
    public int getCapacity(){
        return data.length;
    }

    //检查数组是否为空
    public boolean isEmpty(){
        return size==0;
    }
}

```

###### 3.添加操作

```java
    //向所有元素后添加一个元素
    public void addLast(int e){
        //size是最后一个没有元素的位置，也是数组中实际存在多少个元素
        //当实际个数和容量相等时，数组已经满了
        if(size==data.length){
            throw new IllegalArgumentException("AddLast is failed.Array is full");
        }
        //size是数组中最后一个没有元素的位置
         data[size]=e;
        size++;
    }
    //向所有元素后添加一个元素(复用方法)
    public void addLast(int e){
        add(size,e);
    }
    // 在所有元素前添加一个元素(复用方法)
    public void addFirst(int e){
        add(0,e);
    }
    //在第index的位置插入新的元素e
    public void add(int index,int e){
        if(size==data.length){
            throw new IllegalArgumentException("AddLast is failed.Array is full");
        }
        //index最小只能是0，index大于size的话插入元素，数组里面就不是连续存放元素的情况了，不合法
        if(index<0||index>size){
            throw  new IllegalArgumentException("AddLast is failed.");
        }

        for(int i=size-1;i>=index;i--){
            data[i+1]=data[i];
        }

        data[index]=e;
        size++;
    }
```

###### 4.toString改写，查询操作和修改操作

```java
//获取index索引位置的元素
    int get(int index){
        //size的位置是没有元素的
        if(index<0||index>=size){
            throw new IllegalArgumentException("index is not illegal");
        }
        return data[index];
    }
    //修改index索引位置的元素为e
    void set(int index,int e){
        //size的位置是没有元素的
        if(index<0||index>=size){
            throw new IllegalArgumentException("index is not illegal");
        }
        data[index]=e;
    }
    @Override
    public String toString(){
        StringBuilder res=new StringBuilder();
        res.append(String.format("Array: size=%d,capacity=%d\n",size,data.length));
        res.append('[');
        for(int i=0;i<size;i++){
            res.append(data[i]);
            if(i!=size-1)
            res.append(',');
        }
        res.append(']');
        return res.toString();
    }
```

###### 5.删除，搜索，包含

```java
//查找数组中是否有元素e
    public boolean contain(int e){
        for(int i=0;i<size;i++){
            if(data[i]==e)
                return true;
        }
        return false;
    }
    //查找数组中元素e所在的索引，如果不存在元素e，则返回-1
    public int find(int e){
        for(int i=0;i<size;i++){
            if(data[i]==e)
                return i;
        }
        return -1;
    }
    //从数组中删除index位置的元素，返回删除的元素
    public int remove(int index){
        if(index<0||index>=size){
            throw  new IllegalArgumentException("it is illegal.");
        }
        int ret=data[index];
        for(int i=index+1;i<size;i++){
            data[i-1]=data[i];
        }
        size--;
        return ret;
    }

    //从数组中删除第一个元素，返回删除的元素
    public int removeFirst(){
       return remove(0);
    }
    //从数组中删除最后一个元素，返回删除的元素
    public int removeLast(){
        return remove(size-1);
    }

    //从数组中删除元素e
    public void removeELement(int e){
        int index=find(e);
        if(index!=-1){
            remove(index);
        }
    }
```

###### 6.采用泛型

```java
public class Array<E> {
    private E[] data;
    //实际上有几个元素，capacity是容量：就是最多可以装多少个元素，没有capacity是因为.length可以代替
    private int size;

    //有参构造函数，用户可以根据需要设置容量
    public Array(int capacity){
        data=(E[])new Object[capacity];
        size=0;
    }

    //无参构造函数，用户调用这个构造函数的时候默认的容量是10
    public Array(){
        this(10);
    }

    //获取数组中的元素个数
    public int getSize(){
        return size;
    }

    //获取数组的容量
    public int getCapacity(){
        return data.length;
    }

    //检查数组是否为空
    public boolean isEmpty(){
        return size==0;
    }

    //向所有元素后添加一个元素
//    public void addLast(int e){
//        //size是最后一个没有元素的位置，也是数组中实际存在多少个元素
//        //当实际个数和容量相等时，数组已经满了
//        if(size==data.length){
//            throw new IllegalArgumentException("AddLast is failed.Array is full");
//        }
//        //size是数组中最后一个没有元素的位置
//        data[size]=e;
//        size++;
//    }
    //向所有元素后添加一个元素
    public void addLast(E e){
        add(size,e);
    }
    // 在所有元素前添加一个元素
    public void addFirst(E e){
        add(0,e);
    }
    //在第index的位置插入新的元素e
    public void add(int index,E e){
        if(size==data.length){
            throw new IllegalArgumentException("AddLast is failed.Array is full");
        }
        //index最小只能是0，index大于size的话插入元素，数组里面就不是连续存放元素的情况了，不合法
        if(index<0||index>size){
            throw  new IllegalArgumentException("AddLast is failed.");
        }

        for(int i=size-1;i>=index;i--){
            data[i+1]=data[i];
        }

        data[index]=e;
        size++;
    }
    //获取index索引位置的元素
    public E get(int index){
        //size的位置是没有元素的
        if(index<0||index>=size){
            throw new IllegalArgumentException("index is not illegal");
        }
        return data[index];
    }
    //修改index索引位置的元素为e
    public void set(int index,E e){
        //size的位置是没有元素的
        if(index<0||index>=size){
            throw new IllegalArgumentException("index is not illegal");
        }
        data[index]=e;
    }
    //查找数组中是否有元素e
    public boolean contain(E e){
        for(int i=0;i<size;i++){
            if(data[i].equals(e))
                return true;
        }
        return false;
    }
    //查找数组中元素e所在的索引，如果不存在元素e，则返回-1
    public int find(E e){
        for(int i=0;i<size;i++){
            if(data[i]==e)
                return i;
        }
        return -1;
    }
    //从数组中删除index位置的元素，返回删除的元素
    public E remove(int index){
        if(index<0||index>=size){
            throw  new IllegalArgumentException("it is illegal.");
        }
        E ret=data[index];
        for(int i=index+1;i<size;i++){
            data[i-1]=data[i];
        }
        data[size]=null;//loitering objects 垃圾回收机制
        size--;
        return ret;
    }

    //从数组中删除第一个元素，返回删除的元素
    public E removeFirst(){
       return remove(0);
    }
    //从数组中删除最后一个元素，返回删除的元素
    public E removeLast(){
        return remove(size-1);
    }

    //从数组中删除元素e
    public void removeELement(E e){
        int index=find(e);
        if(index!=-1){
            remove(index);
        }
    }
    @Override
    public String toString(){
        StringBuilder res=new StringBuilder();
        res.append(String.format("Array: size=%d,capacity=%d\n",size,data.length));
        res.append('[');
        for(int i=0;i<size;i++){
            res.append(data[i]);
            if(i!=size-1)
            res.append(',');
        }
        res.append(']');
        return res.toString();
    }


}

```

```java
public class Student {
    private String name;
    private int score;

    public Student(String studentName,int studentScore){
        name=studentName;
        score=studentScore;
    }

    @Override
    public String toString(){
        return String.format("(Student: name%s,score%d)",name,score);
    }

    public static void main(String[] args){
        Array<Student> arr=new Array();
        arr.addLast(new Student("协圳",100));
        arr.addLast(new Student("伟华",100));
        arr.addLast(new Student("崇策",100));
        System.out.println(arr);
    }
}

```

###### 防止复杂度震荡

```java
 //从数组中删除index位置的元素，返回删除的元素
    public E remove(int index){
        if(index<0||index>=size){
            throw  new IllegalArgumentException("it is illegal.");
        }
        E ret=data[index];
        for(int i=index+1;i<size;i++){
            data[i-1]=data[i];
        }
        data[size]=null;//loitering objects 垃圾回收机制
      //不要size等于容量一半的时候就直接缩容为原来的1/2，当size=capacity/4的时候，capacity才除以2
      // data.length/2!=0 有时候capacity会变的很小，比如1，1/2==0 就会失去这个resize的方法和作用
        if(size==data.length/4 && data.length/2!=0){
            resize(data.length/2);
        }
        size--;
        return ret;
    }
```

