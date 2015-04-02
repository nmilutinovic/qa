SQL aggregates
==============

In this segment you will find more advanced concepts using SQL aggregate functions.
You will need to resort to <strong>GROUP BY</strong>, <strong>HAVING</strong> and
aggregate functions themselves: <strong>count()</strong>, <strong>min()</strong>,
<strong>max()</strong> and <strong>avg()</strong>.

<style type="text/css">
	.hidden {
		color: white;
		background-color: white;
		border: solid blue 1px;
		padding-top: 20px;
		position: relative;
	}
	.hidden::before {
		content: "Select to reveal hidden text";
		background-color: blue;
		display: block;
		position: absolute;
		top: 0;
		left: 0;
	}
</style>

Aggregate functions
-------------------
 
Find the number of films where "Judie Cruise" (with ID: 57 is acting)

<div class="hidden">
   select count(*) from sakila.film_actor fa, sakila.film f where fa.actor_id=57 and fa.film_id=f.film_id;
</div>

### Expected result

30

Grouping and counting
---------------------

Find the number of rentals each customer has made, display ID and number of rentals,
sort by number of rentals, ascending.

<div class="hidden">
	SELECT customer_id as ID, count(*) as cnt FROM sakila.rental GROUP BY customer_id ORDER BY cnt;
</div>

### Expected result (first 10 rows)

<table>
	<thead>
		<tr>
			<th>ID</th>
			<th>cnt</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>318</td>
			<td>12</td>
		</tr>
		<tr>
			<td>281</td>
			<td>14</td>
		</tr>
		<tr>
			<td>61</td>
			<td>14</td>
		</tr>
		<tr>
			<td>110</td>
			<td>14</td>
		</tr>
		<tr>
			<td>136</td>
			<td>15</td>
		</tr>
		<tr>
			<td>248</td>
			<td>15</td>
		</tr>
		<tr>
			<td>492</td>
			<td>16</td>
		</tr>
		<tr>
			<td>398</td>
			<td>16</td>
		</tr>
		<tr>
			<td>464</td>
			<td>16</td>
		</tr>
		<tr>
			<td>164</td>
			<td>16</td>
		</tr>
	</tbody>
</table>

Select a minimum of a grouped query result
------------------------------------------

Taking the previous example, try to select only the row(s) with minimum value for
the number of rentals.

Hint: you might need 2 queries for that.
Hint: If you see an error "Every derived table must have its own alias. " check this out [Stackoverflow](http://stackoverflow.com/questions/1888779/every-derived-table-must-have-its-own-alias)

<div class="hidden">
	SELECT customer_id, min(cnt) FROM (SELECT customer_id, count(*) as cnt FROM sakila.rental group by customer_id order by cnt) as q1;
</div>

 







