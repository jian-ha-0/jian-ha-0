 L ist接口概述  
* 鉴于Java中数组用来存储数据的局限性，我们通常使用List替代数组  
* List集合类中元素有序、且可重复，集合中的每个元素都有其对应的顺序索引。  
* List容器中的元素都对应一个整数型的序号记载其在容器中的位置，可以根据  
* 序号存取容器中的元素。  
* JDK API中List接口的实现类常用的有: ArrayList、 LinkedList和Vector。  
*  
*  
*  
* /----Collection接口: 单列集合,用来存储一个一个的对象  
* /----List接口: 存储有序的、可重复的数据。 -->“动态”数组,替换原有的数组  
* -ArrayList: 作为List接口的主要实现类;线程不安全的，效率高;底层使用0bject[] eLementData存储  
* L inkedLst: 对于频繁的插入、删除操作，使用此类效率比ArrayList高; 底层使用双向链表存储  
* /----Vector:作为List接口的古老实现类;线程安全的，效率低;底层使用object[] elementData存储  
*  
*  
* 2. ArrayList 的源码分析:  
* 2.1 jdk 7情况下  
* ArrayList list = new ArrayList();//底层创建了长度是10的Object[]数组e LementData  
* list. add(123);//elementData[e] = new Integer(123);  
* List. add(11);//如果此次的添加导致底层e LementData数组容量不够，则扩容。  
* 默认情况下，扩容为原来的容量的1.5倍，同时需要将原有数组中的数据复制到新的数组中。  
* 结论:建议开发中使用带参的构造器: ArrayList list = new Arraylist(int capacity)  
* 2.2 jdk 8中ArrayList的变化:  
* ArrayList List = new ArrayList();//底层object[] elementData 初始化为{}.并没有创建长度为10的数组  
* list. add(123);//第-次调用add()时，底层才创建了长度10的数组，并将数据123添加到elementData 【10】中  
* 后续的操作和jdk7的一样  
* 2.3小结: jdk7 中的ArrayList的对象的创建类似于单例的饿汉式，而jdk8 中的ArrayList的对象  
* 的创建类似于单例的懒汉式，延迟了数组的创建，节省内存。  
*  
*  
* 3. LinkedList 的源码分析:  
* LinkedList list = new LinkedList(); 内部声明了Node类型的first和ast属性，默认值为null  
* List. add(123); //将123封装到Node中，创建了Node对象。  
* 其中，Node定义为:体现了LinkedList的双向链表的说法  
* private static cLass Node<E> {  
* E item;|  
* Node<E> next;  
* Node<E> prev;  
* Node(Node<E> prev, E element, Node<E> next) {  
* this. item = element;  
* this.next = next;  
* this.prev = prev;  
* }  
*4. Vector 的源码分析: jdk7 和jdk8中通过Vector()构造器创建对象时，底层都创建了长度为10的数组  
* 在扩容方面，默认扩容为原来的数组长度的2倍。  
* 面试题: ArrayList、 LinkedList、 Vector三者的异同?  
* 同:三个类都是实现了List接口，存储数据的特点相同:存储有序的、可重复的数据  
* 不同:见上