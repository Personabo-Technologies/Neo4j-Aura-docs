<div>

<div>

# APOC support

</div>

<div>

<div>

<div>

APOC (Awesome Procedures on Cypher) is a Neo4j library that provides
access to additional procedures and functions, extending the use of the
Cypher query language. For more information on APOC, see the APOC
documentation.

</div>

<div>

A subset of the APOC Core functions and procedures are pre-installed and
available in Aura, as shown below:

</div>

</div>

</div>

<div>

## apoc

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.case <span><i></i></span> </a><br/>
For each pair of conditional and read-only queries in the given list, this procedure will run the first query for which the conditional is evaluated to true.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.help <span><i></i></span> </a><br/>
Returns descriptions of the available APOC procedures and functions.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.version <span><i></i></span> </a><br/>
Returns the APOC version currently installed.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.when <span><i></i></span> </a><br/>
This procedure will run the read-only ifQuery if the conditional has evaluated to true, otherwise the elseQuery will run.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.agg

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.agg.first <span><i></i></span> </a><br/>
Returns the first value from the given collection.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.agg.graph <span><i></i></span> </a><br/>
Returns all distinct nodes and relationships collected into a map with the keys <code>nodes</code> and <code>relationships</code>.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.agg.last <span><i></i></span> </a><br/>
Returns the last value from the given collection.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.agg.maxItems <span><i></i></span> </a><br/>
Returns a map {items:[], value:n} where the <code>value</code> key is the maximum value present, and <code>items</code> represent all items with the same value.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.agg.median <span><i></i></span> </a><br/>
Returns the mathematical median for all non-null numeric values.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.agg.minItems <span><i></i></span> </a><br/>
Returns a map {items:[], value:n} where the <code>value</code> key is the minimum value present, and <code>items</code> represent all items with the same value.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.agg.nth <span><i></i></span> </a><br/>
Returns the nth value in the given collection (to fetch the last item of an unknown length collection, -1 can be used).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.agg.percentiles <span><i></i></span> </a><br/>
Returns the given percentiles over the range of numerical values in the given collection.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.agg.product <span><i></i></span> </a><br/>
Returns the product of all non-null numerical values in the collection.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.agg.slice <span><i></i></span> </a><br/>
Returns a subset of non-null values from the given collection (the collection is considered to be zero-indexed).
To specify the range from start until the end of the collection, the length should be set to -1.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.agg.statistics <span><i></i></span> </a><br/>
Returns the following statistics on the numerical values in the given collection: percentiles, min, minNonZero, max, total, mean, stdev.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.algo

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.algo.aStar <span><i></i></span> </a><br/>
Runs the A* search algorithm to find the optimal path between two nodes, using the given relationship property name for the cost function.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.algo.aStarConfig <span><i></i></span> </a><br/>
Runs the A* search algorithm to find the optimal path between two nodes, using the given relationship property name for the cost function.
This procedure looks for weight, latitude and longitude properties in the config.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.algo.allSimplePaths <span><i></i></span> </a><br/>
Runs a search algorithm to find all of the simple paths between the given relationships, up to a max depth described by maxNodes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.algo.cover <span><i></i></span> </a><br/>
Returns all relationships between a given set of nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.algo.dijkstra <span><i></i></span> </a><br/>
Runs Dijkstra’s algorithm using the given relationship property as the cost function.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.any

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.any.properties <span><i></i></span> </a><br/>
Returns all properties of the given object.
The object can be a virtual node, a real node, a virtual relationship, a real relationship, or a map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.any.property <span><i></i></span> </a><br/>
Returns the property for the given key from an object.
The object can be a virtual node, a real node, a virtual relationship, a real relationship, or a map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.atomic

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.atomic.add <span><i></i></span> </a><br/>
Sets the given property to the sum of itself and the number value.
The procedure then sets the property to the returned sum.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.atomic.concat <span><i></i></span> </a><br/>
Sets the given property to the concatenation of itself and the string value.
The procedure then sets the property to the returned string.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.atomic.insert <span><i></i></span> </a><br/>
Inserts a value at position into the array value of a property.
The procedure then sets the result back on the property.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.atomic.remove <span><i></i></span> </a><br/>
Removes the element at position from the array value of a property.
The procedure then sets the property to the resulting array value.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.atomic.subtract <span><i></i></span> </a><br/>
Sets the property of a value to itself minus the given number value.
The procedure then sets the property to the returned sum.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.atomic.update <span><i></i></span> </a><br/>
Updates the value of a property with a Cypher operation.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.bitwise

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.bitwise.op <span><i></i></span> </a><br/>
Returns the result of the bitwise operation</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.coll

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.coll.avg <span><i></i></span> </a><br/>
Returns the average of the numbers in the list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.combinations <span><i></i></span> </a><br/>
Returns a collection of all combinations of list elements between the selection size minSelect and maxSelect (default: minSelect).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.contains <span><i></i></span> </a><br/>
Returns whether or not the given value exists in the given collection (using a HashSet).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.containsAll <span><i></i></span> </a><br/>
Returns whether or not all of the given values exist in the given collection (using a HashSet).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.containsAllSorted <span><i></i></span> </a><br/>
Returns whether or not all of the given values in the second list exist in an already sorted collection (using a binary search).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.containsDuplicates <span><i></i></span> </a><br/>
Returns true if a collection contains duplicate elements.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.containsSorted <span><i></i></span> </a><br/>
Returns whether or not the given value exists in an already sorted collection (using a binary search).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.different <span><i></i></span> </a><br/>
Returns true if all the values in the given list are unique.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.disjunction <span><i></i></span> </a><br/>
Returns the disjunct set of two lists.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.dropDuplicateNeighbors <span><i></i></span> </a><br/>
Removes duplicate consecutive objects in the list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.duplicates <span><i></i></span> </a><br/>
Returns a list of duplicate items in the collection.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.duplicatesWithCount <span><i></i></span> </a><br/>
Returns a list of duplicate items in the collection and their count, keyed by <code>item</code> and <code>count</code>.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.elements <span><i></i></span> </a><br/>
Deconstructs a list of mixed types into identifiers indicating their specific type.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.fill <span><i></i></span> </a><br/>
Returns a list with the given count of items.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.flatten <span><i></i></span> </a><br/>
Flattens the given list (to flatten nested lists, set recursive to true).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.frequencies <span><i></i></span> </a><br/>
Returns a list of frequencies of the items in the collection, keyed by <code>item</code> and <code>count</code>.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.frequenciesAsMap <span><i></i></span> </a><br/>
Returns a map of frequencies of the items in the collection, keyed by <code>item</code> and <code>count</code>.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.indexOf <span><i></i></span> </a><br/>
Returns the index for the first occurrence of the specified value in the list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.insert <span><i></i></span> </a><br/>
Inserts a value into the specified index in the list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.insertAll <span><i></i></span> </a><br/>
Inserts all of the values into the list, starting at the specified index.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.intersection <span><i></i></span> </a><br/>
Returns the distinct intersection of two lists.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.isEqualCollection <span><i></i></span> </a><br/>
Returns true if the two collections contain the same elements with the same cardinality in any order (using a HashMap).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.max <span><i></i></span> </a><br/>
Returns the maximum of all values in the given list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.min <span><i></i></span> </a><br/>
Returns the minimum of all values in the given list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.occurrences <span><i></i></span> </a><br/>
Returns the count of the given item in the collection.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.pairs <span><i></i></span> </a><br/>
Returns a list of adjacent elements in the list ([1,2],[2,3],[3,null]).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.pairsMin <span><i></i></span> </a><br/>
Returns lists of adjacent elements in the list ([1,2],[2,3]), skipping the final element.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.partition <span><i></i></span> </a><br/>
Partitions the original list into sub-lists of the given batch size.
The final list may be smaller than the given batch size.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.partition <span><i></i></span> </a><br/>
Partitions the original list into sub-lists of the given batch size.
The final list may be smaller than the given batch size.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.randomItem <span><i></i></span> </a><br/>
Returns a random item from the list, or null on an empty or null list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.randomItems <span><i></i></span> </a><br/>
Returns a list of itemCount random items from the original list (optionally allowing elements in the original list to be selected more than once).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.remove <span><i></i></span> </a><br/>
Removes a range of values from the list, beginning at position index for the given length of values.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.removeAll <span><i></i></span> </a><br/>
Returns the first list with all elements of the second list removed.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.runningTotal <span><i></i></span> </a><br/>
Returns an accumulative array.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.set <span><i></i></span> </a><br/>
Sets the element at the given index to the new value.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.shuffle <span><i></i></span> </a><br/>
Returns the list shuffled.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.sort <span><i></i></span> </a><br/>
Sorts the given list into ascending order.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.sortMaps <span><i></i></span> </a><br/>
Sorts the given list into ascending order, based on the map property indicated by <code>prop</code>.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.sortMulti <span><i></i></span> </a><br/>
Sorts the given list of maps by the given fields.
To indicate that a field should be sorted according to ascending values, prefix it with a caret (^).
It is also possible to add limits to the list and to skip values.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.sortNodes <span><i></i></span> </a><br/>
Sorts the given list of nodes by their property into ascending order.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.sortText <span><i></i></span> </a><br/>
Sorts the given list of strings into ascending order.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.split <span><i></i></span> </a><br/>
Splits a collection by the given value. The value itself will not be part of the resulting lists.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.subtract <span><i></i></span> </a><br/>
Returns the first list as a set with all the elements of the second list removed.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.sum <span><i></i></span> </a><br/>
Returns the sum of all the numbers in the list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.sumLongs <span><i></i></span> </a><br/>
Returns the sum of all the numbers in the list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.toSet <span><i></i></span> </a><br/>
Returns a unique list from the given list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.union <span><i></i></span> </a><br/>
Returns the distinct union of the two given lists.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.unionAll <span><i></i></span> </a><br/>
Returns the full union of the two given lists (duplicates included).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.zip <span><i></i></span> </a><br/>
Returns the two given lists zipped together as a list of lists.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.coll.zipToRows <span><i></i></span> </a><br/>
Returns the two lists zipped together, with one row per zipped pair.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.convert

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.convert.fromJsonList <span><i></i></span> </a><br/>
Converts the given JSON list into a Cypher list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.fromJsonMap <span><i></i></span> </a><br/>
Converts the given JSON map into a Cypher map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.getJsonProperty <span><i></i></span> </a><br/>
Converts a serialized JSON object from the property of the given node into the equivalent Cypher structure (e.g. map, list).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.getJsonPropertyMap <span><i></i></span> </a><br/>
Converts a serialized JSON object from the property of the given node into a Cypher map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.setJsonProperty <span><i></i></span> </a><br/>
Serializes the given JSON object and sets it as a property on the given node.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.toJson <span><i></i></span> </a><br/>
Serializes the given JSON value.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.toList <span><i></i></span> </a><br/>
Converts the given value into a list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.toMap <span><i></i></span> </a><br/>
Converts the given value into a map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.toNode <span><i></i></span> </a><br/>
Converts the given value into a node.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.toNodeList <span><i></i></span> </a><br/>
Converts the given value into a list of nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.toRelationship <span><i></i></span> </a><br/>
Converts the given value into a relationship.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.toRelationshipList <span><i></i></span> </a><br/>
Converts the given value into a list of relationships.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.toSet <span><i></i></span> </a><br/>
Converts the given value into a set.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.toSortedJsonMap <span><i></i></span> </a><br/>
Converts a serialized JSON object from the property of a given node into a Cypher map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.convert.toTree <span><i></i></span> </a><br/>
Returns a stream of maps, representing the given paths as a tree with at least one root.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.create

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.create.addLabels <span><i></i></span> </a><br/>
Adds the given labels to the given nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.node <span><i></i></span> </a><br/>
Creates a node with the given dynamic labels.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.nodes <span><i></i></span> </a><br/>
Creates nodes with the given dynamic labels.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.relationship <span><i></i></span> </a><br/>
Creates a relationship with the given dynamic relationship type.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.removeLabels <span><i></i></span> </a><br/>
Removes the given labels from the given node(s).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.removeProperties <span><i></i></span> </a><br/>
Removes the given properties from the given node(s).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.removeRelProperties <span><i></i></span> </a><br/>
Removes the given properties from the given relationship(s).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.setLabels <span><i></i></span> </a><br/>
Sets the given labels to the given node(s). Non-matching labels are removed from the nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.setProperties <span><i></i></span> </a><br/>
Sets the given properties to the given node(s).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.setProperty <span><i></i></span> </a><br/>
Sets the given property to the given node(s).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.setRelProperties <span><i></i></span> </a><br/>
Sets the given properties on the relationship(s).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.setRelProperty <span><i></i></span> </a><br/>
Sets the given property on the relationship(s).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.uuid <span><i></i></span> </a><br/>
Returns a UUID.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.uuids <span><i></i></span> </a><br/>
Returns a stream of UUIDs.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.vNode <span><i></i></span> </a><br/>
Returns a virtual node.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.vNode <span><i></i></span> </a><br/>
Returns a virtual node.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.vNodes <span><i></i></span> </a><br/>
Returns virtual nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.vRelationship <span><i></i></span> </a><br/>
Returns a virtual relationship.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.vRelationship <span><i></i></span> </a><br/>
Returns a virtual relationship.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.create.virtual.fromNode <span><i></i></span> </a><br/>
Returns a virtual node from the given existing node.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.cypher

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.cypher.doIt <span><i></i></span> </a><br/>
Runs a dynamically constructed string with the given parameters.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.cypher.run <span><i></i></span> </a><br/>
Runs a dynamically constructed read-only string with the given parameters.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.cypher.runFirstColumnMany <span><i></i></span> </a><br/>
Runs the given statement with the given parameters and returns the first column collected into a list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.cypher.runFirstColumnSingle <span><i></i></span> </a><br/>
Runs the given statement with the given parameters and returns the first element of the first column.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.cypher.runMany <span><i></i></span> </a><br/>
Runs each semicolon separated statement and returns a summary of the statement outcomes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.cypher.runTimeboxed <span><i></i></span> </a><br/>
Terminates a Cypher statement if it has not finished before the set timeout (ms).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.data

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.data.url <span><i></i></span> </a><br/>
Turns a URL into a map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.date

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.date.add <span><i></i></span> </a><br/>
Adds a unit of specified time to the given timestamp.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.convert <span><i></i></span> </a><br/>
Converts the given timestamp from one time unit into a timestamp of a different time unit.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.convertFormat <span><i></i></span> </a><br/>
Converts a string of one type of date format into a string of another type of date format.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.currentTimestamp <span><i></i></span> </a><br/>
Returns the current Unix epoch timestamp in milliseconds.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.field <span><i></i></span> </a><br/>
Returns the value of one field from the given date time.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.fields <span><i></i></span> </a><br/>
Splits the given date into fields returning a map containing the values of each field.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.format <span><i></i></span> </a><br/>
Returns a string representation of the time value.
The time unit (default: ms), date format (default: ISO), and time zone (default: current time zone) can all be changed.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.fromISO8601 <span><i></i></span> </a><br/>
Converts the given date string (ISO8601) to an integer representing the time value in milliseconds.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.parse <span><i></i></span> </a><br/>
Parses the given date string from a specified format into the specified time unit.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.systemTimezone <span><i></i></span> </a><br/>
Returns the display name of the system time zone (e.g. Europe/London).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.toISO8601 <span><i></i></span> </a><br/>
Returns a string representation of a specified time value in the ISO8601 format.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.date.toYears <span><i></i></span> </a><br/>
Converts the given timestamp or the given date into a floating point representing years.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.diff

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.diff.nodes <span><i></i></span> </a><br/>
Returns a list detailing the differences between the two given nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.do

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.do.case <span><i></i></span> </a><br/>
For each pair of conditional queries in the given list, this procedure will run the first query for which the conditional is evaluated to true.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.do.when <span><i></i></span> </a><br/>
Runs the given read/write ifQuery if the conditional has evaluated to true, otherwise the elseQuery will run.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.example

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.example.movies <span><i></i></span> </a><br/>
Seeds the database with the Neo4j movie dataset.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.export

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.export.csv.all <span><i></i></span> </a><br/>
Exports the full database to the provided CSV file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.csv.data <span><i></i></span> </a><br/>
Exports the given nodes and relationships to the provided CSV file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.csv.graph <span><i></i></span> </a><br/>
Exports the given graph to the provided CSV file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.csv.query <span><i></i></span> </a><br/>
Exports the results from running the given Cypher query to the provided CSV file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.cypher.all <span><i></i></span> </a><br/>
Exports the full database (incl. indexes) as Cypher statements to the provided file (default: Cypher Shell).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.cypher.data <span><i></i></span> </a><br/>
Exports the given nodes and relationships (incl. indexes) as Cypher statements to the provided file (default: Cypher Shell).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.cypher.graph <span><i></i></span> </a><br/>
Exports the given graph (incl. indexes) as Cypher statements to the provided file (default: Cypher Shell).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.cypher.query <span><i></i></span> </a><br/>
Exports the nodes and relationships from the given Cypher query (incl. indexes) as Cypher statements to the provided file (default: Cypher Shell).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.cypher.schema <span><i></i></span> </a><br/>
Exports all schema indexes and constraints to Cypher statements.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.graphml.all <span><i></i></span> </a><br/>
Exports the full database to the provided GraphML file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.graphml.data <span><i></i></span> </a><br/>
Exports the given nodes and relationships to the provided GraphML file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.graphml.graph <span><i></i></span> </a><br/>
Exports the given graph to the provided GraphML file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.graphml.query <span><i></i></span> </a><br/>
Exports the given nodes and relationships from the Cypher statement to the provided GraphML file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.json.all <span><i></i></span> </a><br/>
Exports the full database to the provided JSON file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.json.data <span><i></i></span> </a><br/>
Exports the given nodes and relationships to the provided JSON file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.json.graph <span><i></i></span> </a><br/>
Exports the given graph to the provided JSON file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.export.json.query <span><i></i></span> </a><br/>
Exports the results from the Cypher statement to the provided JSON file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.graph

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.graph.from <span><i></i></span> </a><br/>
Generates a virtual sub-graph by extracting all of the nodes and relationships from the given data.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.graph.fromCypher <span><i></i></span> </a><br/>
Generates a virtual sub-graph by extracting all of the nodes and relationships from the data returned by the given Cypher statement.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.graph.fromDB <span><i></i></span> </a><br/>
Generates a virtual sub-graph by extracting all of the nodes and relationships from the data returned by the given database.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.graph.fromData <span><i></i></span> </a><br/>
Generates a virtual sub-graph by extracting all of the nodes and relationships from the given data.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.graph.fromDocument <span><i></i></span> </a><br/>
Generates a virtual sub-graph by extracting all of the nodes and relationships from the data returned by the given JSON file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.graph.fromPath <span><i></i></span> </a><br/>
Generates a virtual sub-graph by extracting all of the nodes and relationships from the data returned by the given path.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.graph.fromPaths <span><i></i></span> </a><br/>
Generates a virtual sub-graph by extracting all of the nodes and relationships from the data returned by the given paths.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.graph.validateDocument <span><i></i></span> </a><br/>
Validates the JSON file and returns the result of the validation.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.hashing

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.hashing.fingerprint <span><i></i></span> </a><br/>
Calculates a MD5 checksum over a node or a relationship (identical entities share the same checksum).
Unsuitable for cryptographic use-cases.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.hashing.fingerprintGraph <span><i></i></span> </a><br/>
Calculates a MD5 checksum over the full graph.
This function uses in-memory data structures.
Unsuitable for cryptographic use-cases.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.hashing.fingerprinting <span><i></i></span> </a><br/>
Calculates a MD5 checksum over a node or a relationship (identical entities share the same checksum).
Unlike <code>apoc.hashing.fingerprint()</code>, this function supports a number of config parameters.
Unsuitable for cryptographic use-cases.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.import

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.import.csv <span><i></i></span> </a><br/>
Imports nodes and relationships with the given labels and types from the provided CSV file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.import.graphml <span><i></i></span> </a><br/>
Imports a graph from the provided GraphML file.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.json

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.json.path <span><i></i></span> </a><br/>
Returns the given JSON path.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.label

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.label.exists <span><i></i></span> </a><br/>
Returns true or false depending on whether or not the given label exists.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.load

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.load.json <span><i></i></span> </a><br/>
Imports JSON file as a stream of values if the given JSON file is an array.
If the given JSON file is a map, this procedure imports a single value instead.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.load.jsonArray <span><i></i></span> </a><br/>
Loads array from a JSON URL (e.g. web-API) to then import the given JSON file as a stream of values.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.load.xml <span><i></i></span> </a><br/>
Loads a single nested map from an XML URL (e.g. web-API).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.lock

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.lock.all <span><i></i></span> </a><br/>
Acquires a write lock on the given nodes and relationships.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.lock.nodes <span><i></i></span> </a><br/>
Acquires a write lock on the given nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.lock.read.nodes <span><i></i></span> </a><br/>
Acquires a read lock on the given nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.lock.read.rels <span><i></i></span> </a><br/>
Acquires a read lock on the given relationships.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.lock.rels <span><i></i></span> </a><br/>
Acquires a write lock on the given relationships.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.map

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.map.clean <span><i></i></span> </a><br/>
Filters the keys and values contained in the given lists.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.flatten <span><i></i></span> </a><br/>
Flattens nested items in the given map.
This function is the reverse of the <code>apoc.map.unflatten</code> function.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.fromLists <span><i></i></span> </a><br/>
Creates a map from the keys and values in the given lists.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.fromNodes <span><i></i></span> </a><br/>
Returns a map of the given prop to the node of the given label.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.fromPairs <span><i></i></span> </a><br/>
Creates a map from the given list of key-value pairs.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.fromValues <span><i></i></span> </a><br/>
Creates a map from the alternating keys and values in the given list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.get <span><i></i></span> </a><br/>
Returns a value for the given key.
If the given key does not exist, or lacks a default value, this function will throw an exception.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.groupBy <span><i></i></span> </a><br/>
Creates a map of the list keyed by the given property, with single values.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.groupByMulti <span><i></i></span> </a><br/>
Creates a map of the lists keyed by the given property, with the list values.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.merge <span><i></i></span> </a><br/>
Merges the two given maps into one map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.mergeList <span><i></i></span> </a><br/>
Merges all maps in the given list into one map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.mget <span><i></i></span> </a><br/>
Returns a list of values for the given keys.
If one of the keys does not exist, or lacks a default value, this function will throw an exception.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.removeKey <span><i></i></span> </a><br/>
Removes the given key from the map (recursively if recursive is true).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.removeKeys <span><i></i></span> </a><br/>
Removes the given keys from the map (recursively if recursive is true).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.setEntry <span><i></i></span> </a><br/>
Adds or updates the given entry in the map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.setKey <span><i></i></span> </a><br/>
Adds or updates the given entry in the map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.setLists <span><i></i></span> </a><br/>
Adds or updates the given keys/value pairs provided in list format (e.g. [key1, key2],[value1, value2]) in a map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.setPairs <span><i></i></span> </a><br/>
Adds or updates the given key/value pairs (e.g. [key1,value1],[key2,value2]) in a map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.setValues <span><i></i></span> </a><br/>
Adds or updates the alternating key/value pairs (e.g. [key1,value1,key2,value2]) in a map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.sortedProperties <span><i></i></span> </a><br/>
Returns a list of key/value pairs.
The pairs are sorted by alphabetically by key, with optional case sensitivity.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.submap <span><i></i></span> </a><br/>
Returns a sub-map for the given keys.
If one of the keys does not exist, or lacks a default value, this function will throw an exception.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.unflatten <span><i></i></span> </a><br/>
Unflattens items in the given map to nested items.
This function is the reverse of the <code>apoc.map.flatten</code> function.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.updateTree <span><i></i></span> </a><br/>
Adds the data map on each level of the nested tree, where the key-value pairs match.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.map.values <span><i></i></span> </a><br/>
Returns a list of values indicated by the given keys (returns a null value if a given key is missing).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.math

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.math.maxByte <span><i></i></span> </a><br/>
Returns the maximum value of a byte.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.math.maxDouble <span><i></i></span> </a><br/>
Returns the largest positive finite value of type double.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.math.maxInt <span><i></i></span> </a><br/>
Returns the maximum value of an integer.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.math.maxLong <span><i></i></span> </a><br/>
Returns the maximum value of a long.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.math.minByte <span><i></i></span> </a><br/>
Returns the minimum value of a byte.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.math.minDouble <span><i></i></span> </a><br/>
Returns the smallest positive non-zero value of type double.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.math.minInt <span><i></i></span> </a><br/>
Returns the minimum value of an integer.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.math.minLong <span><i></i></span> </a><br/>
Returns the minimum value of a long.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.math.regr <span><i></i></span> </a><br/>
Returns the coefficient of determination (R-squared) for the values of propertyY and propertyX in the given label.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.merge

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.merge.node <span><i></i></span> </a><br/>
Merges the given node(s) with the given dynamic labels.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.merge.node.eager <span><i></i></span> </a><br/>
Merges the given node(s) with the given dynamic labels eagerly.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.merge.relationship <span><i></i></span> </a><br/>
Merges the given relationship(s) with the given dynamic types/properties.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.merge.relationship.eager <span><i></i></span> </a><br/>
Merges the given relationship(s) with the given dynamic types/properties eagerly.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.meta

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.meta.cypher.isType <span><i></i></span> </a><br/>
Returns true if the given value matches the given type.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.meta.cypher.type <span><i></i></span> </a><br/>
Returns the type name of the given value.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.meta.cypher.types <span><i></i></span> </a><br/>
Returns a map containing the type names of the given values.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.meta.data <span><i></i></span> </a><br/>
Examines the full graph and returns a table of metadata.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.meta.graph <span><i></i></span> </a><br/>
Examines the full graph and returns a meta-graph.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.meta.graphSample <span><i></i></span> </a><br/>
Examines the full graph and returns a meta-graph.
Unlike <code>apoc.meta.graph</code>, this procedure does not filter away non-existing paths.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.meta.nodeTypeProperties <span><i></i></span> </a><br/>
Examines the full graph and returns a table of metadata with information about the nodes therein.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.meta.relTypeProperties <span><i></i></span> </a><br/>
Examines the full graph and returns a table of metadata with information about the relationships therein.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.meta.schema <span><i></i></span> </a><br/>
Examines the given sub-graph and returns metadata as a map.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.meta.stats <span><i></i></span> </a><br/>
Returns the metadata stored in the transactional database statistics.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.meta.subGraph <span><i></i></span> </a><br/>
Examines the given sub-graph and returns a meta-graph.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.neighbors

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.neighbors.athop <span><i></i></span> </a><br/>
Returns all nodes connected by the given relationship types at the specified distance.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.neighbors.athop.count <span><i></i></span> </a><br/>
Returns the count of all nodes connected by the given relationship types at the specified distance.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.neighbors.byhop <span><i></i></span> </a><br/>
Returns all nodes connected by the given relationship types within the specified distance.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.neighbors.byhop.count <span><i></i></span> </a><br/>
Returns the count of all nodes connected by the given relationship types within the specified distance.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.neighbors.tohop <span><i></i></span> </a><br/>
Returns all nodes connected by the given relationship types within the specified distance.
Nodes are returned individually for each row.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.neighbors.tohop.count <span><i></i></span> </a><br/>
Returns the count of all nodes connected by the given relationships in the pattern within the specified distance.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.node

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.node.degree <span><i></i></span> </a><br/>
Returns the total degrees for the given node.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.node.degree.in <span><i></i></span> </a><br/>
Returns the total number of incoming relationships to the given node.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.node.degree.out <span><i></i></span> </a><br/>
Returns the total number of outgoing relationships from the given node.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.node.id <span><i></i></span> </a><br/>
Returns the id for the given virtual node.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.node.labels <span><i></i></span> </a><br/>
Returns the labels for the given virtual node.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.node.relationship.exists <span><i></i></span> </a><br/>
Returns a boolean based on whether the given node has a relationship (or whether the given node has a relationship of the given type and direction).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.node.relationship.types <span><i></i></span> </a><br/>
Returns a list of distinct relationship types for the given node.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.node.relationships.exist <span><i></i></span> </a><br/>
Returns a boolean based on whether the given node has relationships (or whether the given nodes has relationships of the given type and direction).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.nodes

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.nodes.collapse <span><i></i></span> </a><br/>
Merges nodes together in the given list.
The nodes are then combined to become one node, with all labels of the previous nodes attached to it, and all relationships pointing to it.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.nodes.connected <span><i></i></span> </a><br/>
Returns true when a given node is directly connected to another given node.
This function is optimized for dense nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.nodes.delete <span><i></i></span> </a><br/>
Deletes all nodes with the given ids.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.nodes.get <span><i></i></span> </a><br/>
Returns all nodes with the given ids.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.nodes.group <span><i></i></span> </a><br/>
Allows for the aggregation of nodes based on the given properties.
This procedure returns virtual nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.nodes.isDense <span><i></i></span> </a><br/>
Returns true if the given node is a dense node.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.nodes.link <span><i></i></span> </a><br/>
Creates a linked list of the given nodes connected by the given relationship type.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.nodes.relationship.types <span><i></i></span> </a><br/>
Returns a list of distinct relationship types from the given list of nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.nodes.relationships.exist <span><i></i></span> </a><br/>
Returns a boolean based on whether or not the given nodes have the given relationships.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.nodes.rels <span><i></i></span> </a><br/>
Returns all relationships with the given ids.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.number

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.number.arabicToRoman <span><i></i></span> </a><br/>
Converts the given Arabic numbers to Roman numbers.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.exact.add <span><i></i></span> </a><br/>
Returns the result of adding the two given large numbers (using Java BigDecimal).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.exact.div <span><i></i></span> </a><br/>
Returns the result of dividing a given large number with another given large number (using Java BigDecimal).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.exact.mul <span><i></i></span> </a><br/>
Returns the result of multiplying two given large numbers (using Java BigDecimal).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.exact.sub <span><i></i></span> </a><br/>
Returns the result of subtracting a given large number from another given large number (using Java BigDecimal).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.exact.toExact <span><i></i></span> </a><br/>
Returns the exact value of the given number (using Java BigDecimal).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.exact.toFloat <span><i></i></span> </a><br/>
Returns the float value of the given large number (using Java BigDecimal).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.exact.toInteger <span><i></i></span> </a><br/>
Returns the integer value of the given large number (using Java BigDecimal).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.format <span><i></i></span> </a><br/>
Formats the given long or double using the given pattern and language to produce a string.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.parseFloat <span><i></i></span> </a><br/>
Parses the given string using the given pattern and language to produce a double.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.parseInt <span><i></i></span> </a><br/>
Parses the given string using the given pattern and language to produce a long.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.number.romanToArabic <span><i></i></span> </a><br/>
Converts the given Roman numbers to Arabic numbers.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.path

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.path.combine <span><i></i></span> </a><br/>
Combines the two given paths into one path.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.path.create <span><i></i></span> </a><br/>
Returns a path from the given start node and a list of relationships.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.path.elements <span><i></i></span> </a><br/>
Converts the given path into a list of nodes and relationships.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.path.expand <span><i></i></span> </a><br/>
Returns paths expanded from the start node following the given relationship types from min-depth to max-depth.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.path.expandConfig <span><i></i></span> </a><br/>
Returns paths expanded from the start node the given relationship types from min-depth to max-depth.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.path.slice <span><i></i></span> </a><br/>
Returns a sub-path of the given length and offset from the given path.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.path.spanningTree <span><i></i></span> </a><br/>
Returns spanning tree paths expanded from the start node following the given relationship types to max-depth.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.path.subgraphAll <span><i></i></span> </a><br/>
Returns the sub-graph reachable from the start node following the given relationship types to max-depth.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.path.subgraphNodes <span><i></i></span> </a><br/>
Returns the nodes in the sub-graph reachable from the start node following the given relationship types to max-depth.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.periodic

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.periodic.cancel <span><i></i></span> </a><br/>
Cancels the given background job.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.periodic.commit <span><i></i></span> </a><br/>
Runs the given statement in separate batched transactions.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.periodic.countdown <span><i></i></span> </a><br/>
Runs a repeatedly called background statement until it returns 0.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.periodic.iterate <span><i></i></span> </a><br/>
Runs the second statement for each item returned by the first statement.
This procedure returns the number of batches and the total number of processed rows.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.periodic.list <span><i></i></span> </a><br/>
Returns a list of all background jobs.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.periodic.repeat <span><i></i></span> </a><br/>
Runs a repeatedly called background job.
To stop this procedure, use <code>apoc.periodic.cancel</code>.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.periodic.submit <span><i></i></span> </a><br/>
Creates a background job which runs the given Cypher statement once.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.refactor

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.refactor.categorize <span><i></i></span> </a><br/>
Creates new category nodes from nodes in the graph with the specified sourceKey as one of its property keys.
The new category nodes are then connected to the original nodes with a relationship of the given type.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.cloneNodes <span><i></i></span> </a><br/>
Clones the given nodes with their labels and properties.
It is possible to skip any node properties using skipProperties (note: this only skips properties on nodes and not their relationships).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.cloneSubgraph <span><i></i></span> </a><br/>
Clones the given nodes with their labels and properties (optionally skipping any properties in the skipProperties list via the config map), and clones the given relationships.
If no relationships are provided, all existing relationships between the given nodes will be cloned.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.cloneSubgraphFromPaths <span><i></i></span> </a><br/>
Clones a sub-graph defined by the given list of paths.
It is possible to skip any node properties using the skipProperties list via the config map.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.collapseNode <span><i></i></span> </a><br/>
Collapses the given node and replaces it with a relationship of the given type.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.extractNode <span><i></i></span> </a><br/>
Expands the given relationships into intermediate nodes.
The intermediate nodes are connected by the given 'OUT' and 'IN' types.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.from <span><i></i></span> </a><br/>
Redirects the given relationship to the given start node.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.invert <span><i></i></span> </a><br/>
Inverts the direction of the given relationship.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.mergeNodes <span><i></i></span> </a><br/>
Merges the given list of nodes onto the first node in the list.
All relationships are merged onto that node as well.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.mergeRelationships <span><i></i></span> </a><br/>
Merges the given list of relationships onto the first relationship in the list.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.normalizeAsBoolean <span><i></i></span> </a><br/>
Refactors the given property to a boolean.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.rename.label <span><i></i></span> </a><br/>
Renames the given label from 'oldLabel' to 'newLabel' for all nodes.
If a list of nodes is provided, the renaming is applied to the nodes within this list only.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.rename.nodeProperty <span><i></i></span> </a><br/>
Renames the given property from 'oldName' to 'newName' for all nodes.
If a list of nodes is provided, the renaming is applied to the nodes within this list only.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.rename.type <span><i></i></span> </a><br/>
Renames all relationships with type 'oldType' to 'newType'.
If a list of relationships is provided, the renaming is applied to the relationships within this list only.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.rename.typeProperty <span><i></i></span> </a><br/>
Renames the given property from 'oldName' to 'newName' for all relationships.
If a list of relationships is provided, the renaming is applied to the relationships within this list only.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.setType <span><i></i></span> </a><br/>
Changes the type of the given relationship.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.refactor.to <span><i></i></span> </a><br/>
Redirects the given relationship to the given end node.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.rel

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.rel.id <span><i></i></span> </a><br/>
Returns the id for the given virtual relationship.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.rel.type <span><i></i></span> </a><br/>
Returns the type for the given virtual relationship.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.schema

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.schema.assert <span><i></i></span> </a><br/>
Drops all other existing indexes and constraints when <code>dropExisting</code> is <code>true</code> (default is <code>true</code>).
Asserts at the end of the operation that the given indexes and unique constraints are there.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.schema.node.constraintExists <span><i></i></span> </a><br/>
Returns a boolean depending on whether or not a constraint exists for the given node label with the given property names.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.schema.node.indexExists <span><i></i></span> </a><br/>
Returns a boolean depending on whether or not an index exists for the given node label with the given property names.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.schema.nodes <span><i></i></span> </a><br/>
Returns all indexes and constraints information for all node labels in the database.
It is possible to define a set of labels to include or exclude in the config parameters.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.schema.properties.distinct <span><i></i></span> </a><br/>
Returns all distinct node property values for the given key.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.schema.properties.distinctCount <span><i></i></span> </a><br/>
Returns all distinct property values and counts for the given key.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.schema.relationship.constraintExists <span><i></i></span> </a><br/>
Returns a boolean depending on whether or not a constraint exists for the given relationship type with the given property names.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.schema.relationships <span><i></i></span> </a><br/>
Returns the indexes and constraints information for all the relationship types in the database.
It is possible to define a set of relationship types to include or exclude in the config parameters.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.scoring

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.scoring.existence <span><i></i></span> </a><br/>
Returns the given score if true, 0 if false.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.scoring.pareto <span><i></i></span> </a><br/>
Applies a Pareto scoring function over the given integers.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.search

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.search.multiSearchReduced <span><i></i></span> </a><br/>
Returns a reduced representation of the nodes found after a parallel search over multiple indexes.
The reduced node representation includes: node id, node labels and the searched properties.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.search.node <span><i></i></span> </a><br/>
Returns all the distinct nodes found after a parallel search over multiple indexes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.search.nodeAll <span><i></i></span> </a><br/>
Returns all the nodes found after a parallel search over multiple indexes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.search.nodeAllReduced <span><i></i></span> </a><br/>
Returns a reduced representation of the nodes found after a parallel search over multiple indexes.
The reduced node representation includes: node id, node labels and the searched properties.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.search.nodeReduced <span><i></i></span> </a><br/>
Returns a reduced representation of the distinct nodes found after a parallel search over multiple indexes.
The reduced node representation includes: node id, node labels and the searched properties.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.spatial

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.spatial.geocode <span><i></i></span> </a><br/>
Returns the geographic location (latitude, longitude, and description) of the given address using a geocoding service (default: OpenStreetMap).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.spatial.geocodeOnce <span><i></i></span> </a><br/>
Returns the geographic location (latitude, longitude, and description) of the given address using a geocoding service (default: OpenStreetMap).
This procedure returns at most one result.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.spatial.reverseGeocode <span><i></i></span> </a><br/>
Returns a textual address from the given geographic location (latitude, longitude) using a geocoding service (default: OpenStreetMap).
This procedure returns at most one result.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.spatial.sortByDistance <span><i></i></span> </a><br/>
Sorts the given collection of paths by the sum of their distance based on the latitude/longitude values on the nodes.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.stats

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.stats.degrees <span><i></i></span> </a><br/>
Returns the percentile groupings of the degrees on the nodes connected by the given relationship types.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.temporal

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.temporal.format <span><i></i></span> </a><br/>
Formats the given temporal value into the given time format.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.temporal.formatDuration <span><i></i></span> </a><br/>
Formats the given duration into the given time format.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.temporal.toZonedTemporal <span><i></i></span> </a><br/>
Parses the given date string using the specified format into the given time zone.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.text

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.text.base64Decode <span><i></i></span> </a><br/>
Decodes the given Base64 encoded string.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.base64Encode <span><i></i></span> </a><br/>
Encodes the given string with Base64.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.base64UrlDecode <span><i></i></span> </a><br/>
Decodes the given Base64 encoded URL.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.base64UrlEncode <span><i></i></span> </a><br/>
Encodes the given URL with Base64.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.byteCount <span><i></i></span> </a><br/>
Returns the size of the given string in bytes.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.bytes <span><i></i></span> </a><br/>
Returns the given string as bytes.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.camelCase <span><i></i></span> </a><br/>
Converts the given string to camel case.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.capitalize <span><i></i></span> </a><br/>
Capitalizes the first letter of the given string.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.capitalizeAll <span><i></i></span> </a><br/>
Capitalizes the first letter of every word in the given string.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.charAt <span><i></i></span> </a><br/>
Returns the long value of the character at the given index.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.clean <span><i></i></span> </a><br/>
Strips the given string of everything except alpha numeric characters and converts it to lower case.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.code <span><i></i></span> </a><br/>
Converts the long value into a string.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.compareCleaned <span><i></i></span> </a><br/>
Compares two given strings stripped of everything except alpha numeric characters converted to lower case.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.decapitalize <span><i></i></span> </a><br/>
Turns the first letter of the given string from upper case to lower case.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.decapitalizeAll <span><i></i></span> </a><br/>
Turns the first letter of every word in the given string to lower case.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.distance <span><i></i></span> </a><br/>
Compares the two given strings using the Levenshtein distance algorithm.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.doubleMetaphone <span><i></i></span> </a><br/>
Returns the double metaphone phonetic encoding of all words in the given string value.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.format <span><i></i></span> </a><br/>
Formats the given string with the given parameters.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.fuzzyMatch <span><i></i></span> </a><br/>
Performs a fuzzy match search of the two given strings.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.hammingDistance <span><i></i></span> </a><br/>
Compares the two given strings using the Hamming distance algorithm.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.hexCharAt <span><i></i></span> </a><br/>
Returns the hexadecimal value of the given string at the given index.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.hexValue <span><i></i></span> </a><br/>
Returns the hexadecimal value of the given value.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.indexOf <span><i></i></span> </a><br/>
Returns the first occurrence of the lookup string in the given string, or -1 if not found.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.indexesOf <span><i></i></span> </a><br/>
Returns all occurences of the lookup string in the given string, or an empty list if not found.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.jaroWinklerDistance <span><i></i></span> </a><br/>
compares the two given strings using the Jaro-Winkler distance algorithm.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.join <span><i></i></span> </a><br/>
Joins the given strings using the given delimiter.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.levenshteinDistance <span><i></i></span> </a><br/>
Compares the given strings using the Levenshtein distance algorithm.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.levenshteinSimilarity <span><i></i></span> </a><br/>
Returns the similarity (a value within 0 and 1) between the two given strings based on the Levenshtein distance algorithm.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.lpad <span><i></i></span> </a><br/>
Left pads the given string by the given width.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.phonetic <span><i></i></span> </a><br/>
Returns the US_ENGLISH phonetic soundex encoding of all words of the string.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.phoneticDelta <span><i></i></span> </a><br/>
Returns the US_ENGLISH soundex character difference between the two given strings.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.random <span><i></i></span> </a><br/>
Generates a random string to the given length using a length parameter and an optional string of valid characters.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.regexGroups <span><i></i></span> </a><br/>
Returns all groups matching the given regular expression in the given text.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.regreplace <span><i></i></span> </a><br/>
Finds and replaces all matches found by the given regular expression with the given replacement.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.repeat <span><i></i></span> </a><br/>
Returns the result of the given item multiplied by the given count.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.replace <span><i></i></span> </a><br/>
Finds and replaces all matches found by the given regular expression with the given replacement.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.rpad <span><i></i></span> </a><br/>
Right pads the given string by the given width.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.slug <span><i></i></span> </a><br/>
Replaces the whitespace in the given string with the given delimiter.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.snakeCase <span><i></i></span> </a><br/>
Converts the given string to snake case.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.sorensenDiceSimilarity <span><i></i></span> </a><br/>
Compares the two given strings using the Sørensen–Dice coefficient formula, with the provided IETF language tag.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.split <span><i></i></span> </a><br/>
Splits the given string using a given regular expression as a separator.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.swapCase <span><i></i></span> </a><br/>
Swaps the cases in the given string.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.toCypher <span><i></i></span> </a><br/>
Converts the given value to a Cypher property string.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.toUpperCase <span><i></i></span> </a><br/>
Converts the given string to upper case.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.upperCamelCase <span><i></i></span> </a><br/>
Converts the given string to upper camel case.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.urldecode <span><i></i></span> </a><br/>
Decodes the given URL encoded string.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.text.urlencode <span><i></i></span> </a><br/>
Encodes the given URL string.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.util

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.util.md5 <span><i></i></span> </a><br/>
Returns the MD5 checksum of the concatenation of all string values in the given list.
MD5 is a weak hashing algorithm which is unsuitable for cryptographic use-cases.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.util.sha1 <span><i></i></span> </a><br/>
Returns the SHA1 of the concatenation of all string values in the given list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.util.sha256 <span><i></i></span> </a><br/>
Returns the SHA256 of the concatenation of all string values in the given list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.util.sha384 <span><i></i></span> </a><br/>
Returns the SHA384 of the concatenation of all string values in the given list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.util.sha512 <span><i></i></span> </a><br/>
Returns the SHA512 of the concatenation of all string values in the list.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.util.sleep <span><i></i></span> </a><br/>
Causes the currently running Cypher to sleep for the given duration of milliseconds (the transaction termination is honored).</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.util.validate <span><i></i></span> </a><br/>
If the given predicate is true an exception is thrown.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
<tr>
<td><div><div>
<p><a>apoc.util.validatePredicate <span><i></i></span> </a><br/>
If the given predicate is true an exception is thrown, otherwise it returns true (for use inside <code>WHERE</code> subclauses).</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.warmup

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.warmup.run <span><i></i></span> </a><br/>
Loads all nodes and relationships in the database into memory.</p>
</div></div></td>
<td><div><div>
<p><span>Procedure</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div>

## apoc.xml

<div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Qualified Name</th>
<th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<p><a>apoc.xml.parse <span><i></i></span> </a><br/>
Parses the given XML string as a map.</p>
</div></div></td>
<td><div><div>
<p><span>Function</span></p>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

</div>
