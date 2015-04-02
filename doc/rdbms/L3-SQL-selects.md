# Exercise 3: Various selects

These are simple selects and some joins.

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

## Simple select criterion

Find a movie named "CAMELOT VACATION", select all of its fields. Note the ID.
(Hint: query window is in global namespace, you need to prefix your table name with a schema name)

<div class="hidden">
	select * from sakila.film where title = 'CAMELOT VACATION';
</div>

### Expected result

film_id,title,description,release_year,language_id,original_language_id,rental_duration,rental_rate,length,replacement_cost,rating,special_features,last_update
114,"CAMELOT VACATION","A Touching Character Study of a Woman And a Waitress who must Battle a Pastry Chef in A MySQL Convention",2006,1,NULL,3,0.99,61,26.99,NC-17,"Trailers,Commentaries,Deleted Scenes,Behind the Scenes","2006-02-15 05:03:42"

## Simple join
   
List all actors in that movie.

<div class="hidden">
   select * from sakila.actor a, sakila.film_actor fa where fa.film_id=114 and fa.actor_id=a.actor_id;
</div>

### Expected result

   57	JUDE	CRUISE	2006-02-15 04:34:33	57	114	2006-02-15 05:05:03
   125	ALBERT	NOLTE	2006-02-15 04:34:33	125	114	2006-02-15 05:05:03

## Join with projection
   
List all actors in that movie, showing only: actor ID, name, surname

<div class="hidden">
   select a.actor_id, a.first_name, a.last_name from sakila.actor a, sakila.film_actor fa where fa.film_id=114 and fa.actor_id=a.actor_id;
</div>

<table>
	<thead>
		<tr>
			<th>actor_id</th>
		</tr>
		<tr>
			<th>first_name</th>
		</tr>
		<tr>
			<th>last_name"</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>57</td>
			<td>JUDE</td>
			<td>CRUISE</td>
		</tr>
		<tr>
			<td>125</td>
			<td>ALBERT</td>
			<td>NOLTE</td>
		</tr>
   </tbody>
</table>

## Join with projection and column renaming
   
Same as previous, just give columns nice names: "ID", "First name", "Last name"

<div class="hidden">
   select a.actor_id as 'ID', a.first_name as 'First name', a.last_name as 'Last name' from sakila.actor a, sakila.film_actor fa where fa.film_id=114 and fa.actor_id=a.actor_id;
</div>

### Expected result
<table>
	<thead>
		<tr>
			<th>ID</th>
		</tr>
		<tr>
			<th>"First name"</th>
		</tr>
		<tr>
			<th>"Last name"</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>57</td>
			<td>JUDE</td>
			<td>CRUISE</td>
		</tr>
		<tr>
			<td>125</td>
			<td>ALBERT</td>
			<td>NOLTE</td>
		</tr>
   </tbody>
</table>

## Joins again
   
List all films where "Judie Cruise" with ID: 57 is acting

<div class="hidden">
   select * from sakila.film_actor fa, sakila.film f where fa.actor_id=57 and fa.film_id=f.film_id;
</div>
   
### Expected result

actor_id,film_id,last_update,film_id,title,description,release_year,language_id,original_language_id,rental_duration,rental_rate,length,replacement_cost,rating,special_features,last_update
57,16,"2006-02-15 05:05:03",16,"ALLEY EVOLUTION","A Fast-Paced Drama of a Robot And a Composer who must Battle a Astronaut in New Orleans",2006,1,NULL,6,2.99,180,23.99,NC-17,"Trailers,Commentaries","2006-02-15 05:03:42"
57,34,"2006-02-15 05:05:03",34,"ARABIA DOGMA","A Touching Epistle of a Madman And a Mad Cow who must Defeat a Student in Nigeria",2006,1,NULL,6,0.99,62,29.99,NC-17,"Commentaries,Deleted Scenes","2006-02-15 05:03:42"
57,101,"2006-02-15 05:05:03",101,"BROTHERHOOD BLANKET","A Fateful Character Study of a Butler And a Technical Writer who must Sink a Astronaut in Ancient Japan",2006,1,NULL,3,0.99,73,26.99,R,"Behind the Scenes","2006-02-15 05:03:42"
57,114,"2006-02-15 05:05:03",114,"CAMELOT VACATION","A Touching Character Study of a Woman And a Waitress who must Battle a Pastry Chef in A MySQL Convention",2006,1,NULL,3,0.99,61,26.99,NC-17,"Trailers,Commentaries,Deleted Scenes,Behind the Scenes","2006-02-15 05:03:42"
57,122,"2006-02-15 05:05:03",122,"CARRIE BUNCH","A Amazing Epistle of a Student And a Astronaut who must Discover a Frisbee in The Canadian Rockies",2006,1,NULL,7,0.99,114,11.99,PG,"Trailers,Commentaries,Behind the Scenes","2006-02-15 05:03:42"
57,134,"2006-02-15 05:05:03",134,"CHAMPION FLATLINERS","A Amazing Story of a Mad Cow And a Dog who must Kill a Husband in A Monastery",2006,1,NULL,4,4.99,51,21.99,PG,Trailers,"2006-02-15 05:03:42"
57,144,"2006-02-15 05:05:03",144,"CHINATOWN GLADIATOR","A Brilliant Panorama of a Technical Writer And a Lumberjack who must Escape a Butler in Ancient India",2006,1,NULL,7,4.99,61,24.99,PG,"Trailers,Commentaries,Deleted Scenes","2006-02-15 05:03:42"
57,153,"2006-02-15 05:05:03",153,"CITIZEN SHREK","A Fanciful Character Study of a Technical Writer And a Husband who must Redeem a Robot in The Outback",2006,1,NULL,7,0.99,165,18.99,G,"Commentaries,Deleted Scenes","2006-02-15 05:03:42"
57,192,"2006-02-15 05:05:03",192,"CROSSING DIVORCE","A Beautiful Documentary of a Dog And a Robot who must Redeem a Womanizer in Berlin",2006,1,NULL,4,4.99,50,19.99,R,"Commentaries,Deleted Scenes,Behind the Scenes","2006-02-15 05:03:42"
57,213,"2006-02-15 05:05:03",213,"DATE SPEED","A Touching Saga of a Composer And a Moose who must Discover a Dentist in A MySQL Convention",2006,1,NULL,4,0.99,104,19.99,R,Commentaries,"2006-02-15 05:03:42"
57,258,"2006-02-15 05:05:03",258,"DRUMS DYNAMITE","A Epic Display of a Crocodile And a Crocodile who must Confront a Dog in An Abandoned Amusement Park",2006,1,NULL,6,0.99,96,11.99,PG,Trailers,"2006-02-15 05:03:42"
57,267,"2006-02-15 05:05:03",267,"EAGLES PANKY","A Thoughtful Story of a Car And a Boy who must Find a A Shark in The Sahara Desert",2006,1,NULL,4,4.99,140,14.99,NC-17,"Trailers,Commentaries,Behind the Scenes","2006-02-15 05:03:42"
57,317,"2006-02-15 05:05:03",317,"FIREBALL PHILADELPHIA","A Amazing Yarn of a Dentist And a A Shark who must Vanquish a Madman in An Abandoned Mine Shaft",2006,1,NULL,4,0.99,148,25.99,PG,"Trailers,Commentaries,Behind the Scenes","2006-02-15 05:03:42"
57,340,"2006-02-15 05:05:03",340,"FRONTIER CABIN","A Emotional Story of a Madman And a Waitress who must Battle a Teacher in An Abandoned Fun House",2006,1,NULL,6,4.99,183,14.99,PG-13,"Commentaries,Deleted Scenes","2006-02-15 05:03:42"
57,393,"2006-02-15 05:05:03",393,"HALLOWEEN NUTS","A Amazing Panorama of a Forensic Psychologist And a Technical Writer who must Fight a Dentist in A U-Boat",2006,1,NULL,6,2.99,47,19.99,PG-13,"Deleted Scenes","2006-02-15 05:03:42"
57,437,"2006-02-15 05:05:03",437,"HOUSE DYNAMITE","A Taut Story of a Pioneer And a Squirrel who must Battle a Student in Soviet Georgia",2006,1,NULL,7,2.99,109,13.99,R,"Commentaries,Deleted Scenes,Behind the Scenes","2006-02-15 05:03:42"
57,447,"2006-02-15 05:05:03",447,"ICE CROSSING","A Fast-Paced Tale of a Butler And a Moose who must Overcome a Pioneer in A Manhattan Penthouse",2006,1,NULL,5,2.99,131,28.99,R,"Deleted Scenes","2006-02-15 05:03:42"
57,502,"2006-02-15 05:05:03",502,"KNOCK WARLOCK","A Unbelieveable Story of a Teacher And a Boat who must Confront a Moose in A Baloon",2006,1,NULL,4,2.99,71,21.99,PG-13,Trailers,"2006-02-15 05:03:42"
57,592,"2006-02-15 05:05:03",592,"MONSTER SPARTACUS","A Fast-Paced Story of a Waitress And a Cat who must Fight a Girl in Australia",2006,1,NULL,6,2.99,107,28.99,PG,"Commentaries,Behind the Scenes","2006-02-15 05:03:42"
57,605,"2006-02-15 05:05:03",605,"MULHOLLAND BEAST","A Awe-Inspiring Display of a Husband And a Squirrel who must Battle a Sumo Wrestler in A Jet Boat",2006,1,NULL,7,2.99,157,13.99,PG,"Trailers,Deleted Scenes,Behind the Scenes","2006-02-15 05:03:42"
57,637,"2006-02-15 05:05:03",637,"OPEN AFRICAN","A Lacklusture Drama of a Secret Agent And a Explorer who must Discover a Car in A U-Boat",2006,1,NULL,7,4.99,131,16.99,PG,"Trailers,Commentaries","2006-02-15 05:03:42"
57,685,"2006-02-15 05:05:03",685,"PLATOON INSTINCT","A Thrilling Panorama of a Man And a Woman who must Reach a Woman in Australia",2006,1,NULL,6,4.99,132,10.99,PG-13,"Trailers,Commentaries","2006-02-15 05:03:42"
57,707,"2006-02-15 05:05:03",707,"QUEST MUSSOLINI","A Fateful Drama of a Husband And a Sumo Wrestler who must Battle a Pastry Chef in A Baloon Factory",2006,1,NULL,5,2.99,177,29.99,R,"Behind the Scenes","2006-02-15 05:03:42"
57,714,"2006-02-15 05:05:03",714,"RANDOM GO","A Fateful Drama of a Frisbee And a Student who must Confront a Cat in A Shark Tank",2006,1,NULL,6,2.99,73,29.99,NC-17,Trailers,"2006-02-15 05:03:42"
57,717,"2006-02-15 05:05:03",717,"REAR TRADING","A Awe-Inspiring Reflection of a Forensic Psychologist And a Secret Agent who must Succumb a Pastry Chef in Soviet Georgia",2006,1,NULL,6,0.99,97,23.99,NC-17,"Trailers,Commentaries,Deleted Scenes","2006-02-15 05:03:42"
57,737,"2006-02-15 05:05:03",737,"ROCK INSTINCT","A Astounding Character Study of a Robot And a Moose who must Overcome a Astronaut in Ancient India",2006,1,NULL,4,0.99,102,28.99,G,"Trailers,Commentaries,Deleted Scenes,Behind the Scenes","2006-02-15 05:03:42"
57,767,"2006-02-15 05:05:03",767,"SCALAWAG DUCK","A Fateful Reflection of a Car And a Teacher who must Confront a Waitress in A Monastery",2006,1,NULL,6,4.99,183,13.99,NC-17,"Commentaries,Behind the Scenes","2006-02-15 05:03:42"
57,852,"2006-02-15 05:05:03",852,"STRANGELOVE DESIRE","A Awe-Inspiring Panorama of a Lumberjack And a Waitress who must Defeat a Crocodile in An Abandoned Amusement Park",2006,1,NULL,4,0.99,103,27.99,NC-17,"Trailers,Commentaries,Deleted Scenes","2006-02-15 05:03:42"
57,891,"2006-02-15 05:05:03",891,"TIMBERLAND SKY","A Boring Display of a Man And a Dog who must Redeem a Girl in A U-Boat",2006,1,NULL,3,0.99,69,13.99,G,Commentaries,"2006-02-15 05:03:42"
57,918,"2006-02-15 05:05:03",918,"TWISTED PIRATES","A Touching Display of a Frisbee And a Boat who must Kill a Girl in A MySQL Convention",2006,1,NULL,4,4.99,152,23.99,PG,"Trailers,Commentaries,Deleted Scenes","2006-02-15 05:03:42"
   
## N-way joins

What categories of films did "GARY PHOENIX" act in?

<div class="hidden">
   select distinct c.name as 'Category'
       <br />
       from sakila.actor a, sakila.film_actor fa, sakila.film f, sakila.film_category fc, sakila.category c
       <br />
       where a.first_name='GARY' and a.last_name='PHOENIX'
           <br />
	       and a.actor_id=fa.actor_id
	       <br />
		   and fa.film_id=f.film_id
		   <br />
		   and fc.film_id=f.film_id
		   <br />
           and fc.category_id=c.category_id;
</div>

### Expected result

<table>
	<thead>
		<tr>
			<th>Category</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Family</td>
		</tr>
		<tr>
			<td>Travel</td>
		</tr>
		<tr>
			<td>Foreign</td>
		</tr>
		<tr>
			<td>Animation</td>
		</tr>
		<tr>
			<td>Sci-Fi</td>
		</tr>
		<tr>
			<td>Action</td>
		</tr>
		<tr>
			<td>Games</td>
		</tr>
		<tr>
			<td>Sports</td>
		</tr>
		<tr>
			<td>New</td>
		</tr>
		<tr>
			<td>Classics</td>
		</tr>
		<tr>
			<td>Documentary</td>
		</tr>
		<tr>
			<td>Horror</td>
		</tr>
		<tr>
			<td>Children</td>
		</tr>
	</tbody>
</table>