# FansubDB's data

Json data of the website [https://fansubdb.github.io](https://fansubdb.github.io).

## Issues

In case of problem, you can add or watch issues [here](https://github.com/FansubDB/fansubdb.github.io/issues).

## License

Theses JSON files, which contain data, are under the [CC BY-SA 4.0 license][CCBYSA].

[CCBYSA]: http://creativecommons.org/licenses/by-sa/4.0/

## API

You can access to our data over **GET** on **HTTPS**. You can see method and structure build in this website: https://fansubdb.github.io/data/

To sum up: you can access to our data with: `fansubdb.github.io/data/:lang/:years/:season.json`
<br>
* `:lang` can be found on `https://fansubdb.github.io/data/lang.json`
* `:year` and `:season` can be found on `https://fansubdb.github.io/data/:lang/list.json` (`:lang` come from above)

#### lang.json, year.json, season.json

* `lang.json` is in the root folder, to choose the subs language.
* `list.json` is in the `:lang` folder. It indicates where the json file of the season animes is located.

They have an object table. The object contains each value (lang/year/season) and their url.

#### The json file of the season animes (AnimeoftheSeason structure)

This file is located under `:lang/:year/:season.json`. (eg. [`data/fr/2014/automne.json`][automne2014JSON])

It's a unique object which contains:

* *`name_lbl`*: Translation of the name; **required**; it's the `<th>` of the table
* *`group_lbl`*: Translation of the group; **required**; it's the second `<th>` of the table
* *`tv_lbl`*: The label of the button to show `TV` list; **required**
* *`ova_lbl`*: The label of the button to show `OVA/ONA/Special` list; **required**
* *`movie_lbl`*: The label of the button to show `Movie` list; **required**
* *`message_empty_list`*: Show the text when the array `tv`,`ova` or `movie` is empty (i.e. contains 0 value)
* *`tv`*: an array of anime objects; **required**; it's the `TV` list
* *`ova`*: an array of anime objects; **required**; it's the `OVA/ONA/Special` list
* *`movie`*: an array of anime objects; **required**; it's the `Movie` list

##### The Anime object (Anime structure)

An anime object contains:

* *`name`*: **required**; it's the `<td>` of the table, appears in the colum of `name`
* *`image`* from MyAnimeList CDN URL link; **required**; show it when click on the button
* *`groups`* (array) of subs-group which subs it: **required**. An object `group` can have:
	* a *`status`* (uncertain, planned, release, dropped, simulcast): **required** if `detail` exists (see below);
	* an array named *`detail`*, where we have the possibility to add co-subbing: **required** if `status` exists. This array contains:
		* the *`name`* of the group: **required** if `status` exists

##### Simple example of a JSON file

```json
{
	"name_lbl": "name",
	"group_lbl": "fansub group",
	"tv_lbl": "TV",
	"ova_lbl": "OVA/ONA/Special",
	"movie_lbl": "Movie",
	"message_empty_list": "This list is empty! <br>Don't hesitate to submit a PR.",
	"tv": [{
		"name": "Anime A",
		"image": "link from CDN MAL of the picture of Anime A",
		"groups": [{
			"status": "release",
			"detail": [{
				"name": "SUBS 1"
			}]
		}]
	}, {
		"name": "Anime B",
		"image": "link from CDN MAL of the picture of Anime B",
		"groups": [{
			"status": "simulcast",
			"detail": [{
				"name": "simulcast 2"
			}]
		}, {
			"status": "dropped",
			"detail": [{
				"name": "fansub drop 1"
			}, {
				"name": "fansub drop 2 in co-subbing with fansub drop 1"
			}]
		}]
	}],
	"ova": [{
		"name": "Anime C",
		"image": "link from CDN MAL of the picture of Anime C",
		"groups": [{
			"status": "release",
			"detail": [{
				"name": "SUBS 1"
			}, {
				"name": "SUBS 2 in co-subbing with SUBS 1"
			}]
		}]
	}, {
		"name": "Anime D",
		"image": "link from CDN MAL of the picture of Anime D",
		"groups": [{
			"status": "planned",
			"detail": [{
				"name": "fansub plan 4"
			}]
		}, {
			"status": "simulcast",
			"detail": [{
				"name": "simulcast 3"
			}]
		}]
	}],
	"movie": [{
		"name": "movie 1",
		"image": "link from CDN MAL of the picture of Movie 1",
		"groups": [{
			"status": "release",
			"detail": [{
				"name": "release group 1"
			}]
		}]
	}, {
		"name": "movie 2",
		"image": "link from CDN MAL of the picture of Movie 2",
		"groups": [{
			"status": "release",
			"detail": [{
				"name": "fansub D"
			}]
		}]
	}]
}
```

[automne2014JSON]: https://fansubdb.github.io/data/fr/2014/automne.json
