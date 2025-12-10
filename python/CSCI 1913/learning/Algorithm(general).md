***Huffman compression***
- Basic compression idea:
	- Given data represented as some quantity of bits, compression transforms the data to use fewer bits. Compressed data uses less storage and can be communicated faster than uncompressed data.
	- The basic idea of compression is to encode frequently-occurring items using fewer bits. Ex: Uncompressed ASCII characters use 8 bits each, but compression uses fewer than 8 bits for more frequently occurring characters.




***

***Heuristics***
```cpp
Knapsack01(knapsack, itemList, itemListSize){
	Sort itemList descending by value;
	remaining = knapsack->maximumWeight;
	
	for(i = 0; i < itemListSize; i++ ){
		if(itemList[i]->weight <= remaining){
		Put itemList[i] in knapsack;
		remaining -= itemList[i]->weight;
	}else{
		break;
	}
}
```

***
***Greedy Algorithm***
- A greedy algorithm is an algorithm that, when presented with a list of options, chooses the option that is optimal at that point in time. The choice of option does not consider additional subsequent options, and may or may not lead to an optimal solution.

***
***Dynamic Programming***
- Dynamic programming is a problem solving technique that splits a problem into smaller subproblems, computes and stores solutions to subproblems in memory, and then uses the stored solutions to solve the larger problem.

| The information provided |             Confirm             |          Unconfirm           |
| :----------------------: | :-----------------------------: | :--------------------------: |
|   The largest value: L   | The length of overlapped string |     position and content     |
| The position: ( i ,  j ) |    The ended index of string    | length, begin index, content |
