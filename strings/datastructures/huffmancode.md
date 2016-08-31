# Huffmancode
```
/**
 * @author: Xavier Geerinck
 * @title: Huffman encoding
 * @subtitle: This algorithm compresses a string it's binary representation
 * @method:
 * 1. Create a table for each character with their "frequence of occurence"
 * 2. Create leaf element of each character and put it in a priority queue (the priority is based on the "frequence of occurence" for that character)
 * 3. As long as the queue >= 2 elements
 *     i. Remove 2 nodes
 *     ii. Make a new node with the 2 children the 2 removed nodes. This new node has the sum of the priorities. (biggest child left, smallest right).
 *     iii. Add this new node to the queue
 * 4. Once we have this tree we can find the huffman code by searching for our value and if we go left, we write a "0" and if we go right we write a "1"
 * @note: performance can be increased by merging some methods (such as textToBinary and createOccurenceTable) but for reading purposes it has been split off.
 */

/**
 * A simple node implementation
 */
function Node(key, priority, left, right) {
    this._left = left || null;
    this._right = right || null;
    this._key = key || "";
    this._priority = priority || 0;
};

Node.prototype.getLeft = function () {
    return this._left;
};

Node.prototype.getRight = function () {
    return this._right;
};

Node.prototype.getKey = function () {
    return this._key;
};

Node.prototype.getPriority = function () {
    return this._priority;
};

Node.prototype.setRight = function (right) {
    this._right = right;
};

Node.prototype.setLeft = function (left) {
    this._left = left;
};

Node.prototype.setKey = function (key) {
    return this._key;
};

Node.prototype.setPriority = function (priority) {
    this._priority = priority;
};

/**
 * A simple priority queue implementation
 */
function PriorityQueue(comparator) {
    this._items = [];
    this._comparator = comparator;
};

PriorityQueue.prototype.size = function () {
    return this._items.length;
};

PriorityQueue.prototype.isEmpty = function () {
    return this.size() == 0;
};

PriorityQueue.prototype.peek = function () {
    if (this.isEmpty()) {
        throw new Error('PriorityQueue is empty');
    }
    
    return this._items[0];
};

PriorityQueue.prototype.dequeue = function () {
    var self = this;
    var item = this._items[0];
    
    this._items = this._items.slice(1, self.size());
    
    return item;
};

PriorityQueue.prototype.enqueue = function (element) {
    var size = this._items.push(element);
    var current = size - 1;
    
    while (current > 0) {
        //var parent = Math.floor((current - 1) / 2);
        var parent = current - 1;
        
        if (this._compare(current, parent) <= 0) break;
        
        this._swap(parent, current);
        current = parent;
    }
    
    return size;
};

PriorityQueue.prototype.print = function () {
    console.log(this._items);
};

PriorityQueue.prototype._compare = function (a, b) {
    return this._comparator(this._items[a], this._items[b]);
};

PriorityQueue.prototype._swap = function (a, b) {
    var aux = this._items[a];
    this._items[a] = this._items[b];
    this._items[b] = aux;
};

/**
 * Huffman Code Algorith + Utils
 */
function textToBinary(input) {
    var result = "";
    
    for (var i = 0; i < input.length; i++) {
        result += input[i].charCodeAt(0).toString(2);
    }
    
    return result;
}

function createOccurenceTable(input) {
    var table = {};
    
    for (var i = 0; i < input.length; i++) {
        if (!table[input[i]]) {
            table[input[i]] = 1;
        } else {
            table[input[i]]++;
        }
    }
    
    return table;
}

function createHuffmanTable(text, huffmanTree) {
    var occurenceTable = createOccurenceTable(text);
    // TODO
}

function createHuffmanTree(input) {
    var occurenceTable = createOccurenceTable(input);
    
    var queue = new PriorityQueue(function (a, b) {
        console.log("Comparing: " + a.getPriority() + " to " + b.getPriority());
        return a.getPriority() < b.getPriority();
    });
    
    // Queue every character
    var occurenceTableKeys = Object.keys(occurenceTable);
    
    for (var i = 0; i < occurenceTableKeys.length; i++) {
        queue.enqueue(new Node(occurenceTableKeys[i], occurenceTable[occurenceTableKeys[i]]));
    }
    
    //queue.print();
    
    // As long as the queue >= 2 elements, continue
    while (queue.size() >= 2) {
        // Get Items
    		var itemA = queue.dequeue();
        var itemB = queue.dequeue();
        
        // Create node
        var newNode = new Node(null, itemA.getPriority() + itemB.getPriority());
        
        // Set largest node left and smallest right
        if (itemA.getPriority() > itemB.getPriority) {
            newNode.setLeft(itemA);
            newNode.setRight(itemB);
        } else {
            newNode.setLeft(itemB);
            newNode.setRight(itemA);
        }
        
        // Push on the queue
        queue.enqueue(newNode);
    }
    
    return queue.peek();
}

var text = "Lorem ipsum dolor sit amet, consectetur adipiscing elit.";
var huffmanTree = createHuffmanTree(text);

var huffmanTable = createHuffmanTable(huffmanTree);

var result = "";
for (var i = 0; i < text.length; i++) {
    result += huffmanTable[text[i]];
}


document.querySelector("#result").innerHTML = "Normal: <br />" + textToBinary(text) + "<br /><br />Huffman Compressed: <br />" + result;
```
