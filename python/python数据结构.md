## List
```python
class ListNode:
	def__init__(self, val):
		self.x = x
		self.next = None
遍历数组
head = createLinkedList([1,2,3,4,5])
p = head
while p is not None:
	print(p.val)
	p = p.next
在单链表头部插入一个新节点 0 
newNode = ListNode(0) 
newNode.next = head 
head = newNode
插入到尾部节点
while p is not None:
	p = p.next
p.next = ListNode()
在中间位置插入
p = head 
for _ in range(2): p = p.next
new_node = ListNode(66) 
new_node.next = p.next
p.next = new_node

删除尾节点
p.next = None;
删除中间节点
p,next = p.next.next;
删除头节点
head = head.next;
```

## Doubly ListNode
```python
class DoublyListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
        self.prev = None
        
def createDoublyLinkedList(arr: List[int]) -> Optional[DoublyListNode]:
    if not arr:
        return None
    
    head = DoublyListNode(arr[0])
    cur = head
    
    # for 循环迭代创建双链表
    for val in arr[1:]:
        new_node = DoublyListNode(val)
        cur.next = new_node
        new_node.prev = cur
        cur = cur.next
    return head
    
# 创建一条双链表
head = createDoublyLinkedList([1, 2, 3, 4, 5])
tail = None
# 从头节点向后遍历双链表
p = head
while p:
    print(p.val)
    tail = p
    p = p.next
# 从尾节点向前遍历双链表
p = tail
while p:
    print(p.val)
    p = p.prev
```