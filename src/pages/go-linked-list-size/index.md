---
title: Find The Number Of Items In A Linked List
date: 2018-11-21 7:00:00
featuredImage: './linkedlist.jpg'
---
A common questions that comes up in coding interviews is to count the number of items in the linked list. Now most list libraries have away to get the size but this cannot be used in a interview.


__Singly Linked List__

Here is a simple linked list implementation that has two functions First which returns the head and Add that adds a new node to the end of the list.

[GitHub Source](https://github.com/harrisonbrock/go-data-structures/tree/master/linked-list)
```go
type List struct {
	head *Node
	tail *Node
}

// Get head / first
func (list *List) First() *Node {
	return list.head

}

// Add
func (list *List) Add(value int) {
	newNode := &Node{data: value}

	if list.head == nil {
		list.head = newNode
	} else {
		list.tail.next = newNode
	}
	list.tail = newNode
}
```
__Solution__

```go
func size(list *List) int {

	// create variable for size
	var size int

	// set current node to head
	current := list.head

	// loop until current is nil
	for current != nil {
		// increase size by  1
		size++
		// set current to next node
		current = current.next
	}
	// return size
	return size
}
```
