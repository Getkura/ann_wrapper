# ann_wrapper


[![Gem Version](https://badge.fury.io/rb/ann_wrapper.png)](http://badge.fury.io/rb/ann_wrapper)
[![Build Status](https://travis-ci.org/shawntoffel/ann_wrapper.png?branch=dev)](https://travis-ci.org/shawntoffel/ann_wrapper)
[![Dependency Status](https://gemnasium.com/badges/github.com/shawntoffel/ann_wrapper.svg)](https://gemnasium.com/github.com/shawntoffel/ann_wrapper)
[![Code Climate](https://codeclimate.com/github/Getkura/ann_wrapper/badges/gpa.svg)](https://codeclimate.com/github/Getkura/ann_wrapper)
[![Coverage Status](https://coveralls.io/repos/github/shawntoffel/ann_wrapper/badge.svg?branch=dev)](https://coveralls.io/github/shawntoffel/ann_wrapper?branch=master)

A simple ruby wrapper/abstraction for the [Anime News Network API](http://www.animenewsnetwork.com/encyclopedia/api.php)

## Installation

Add this line to your application's Gemfile:

    gem 'ann_wrapper'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install ann_wrapper

## Usage

###Fetch an anime:

    anime = ANN_Wrapper.fetch_anime "id"
    anime.title
    anime.alt_titles
    anime.synopsis
    anime.num_episodes
    anime.genres
    anime.themes
    anime.vintage
    anime.op_theme
    anime.ed_theme
    anime.id
    anime.type
    anime.ratings
    anime.episodes
    anime.staff
    anime.cast
    anime.images
    anime.to_h
    
####Example:

    steins_gate = ANN_Wrapper.fetch_anime 11770

#####Info:

    steins_gate.id
     => "11770"

    steins_gate.title
     => ["Steins;Gate"]

    steins_gate.alt_titles
     => {"PT"=>["Steins-Gate e a Teoria do Caos"], "JA"=>["シュタインズ・ゲート"], "ZH-TW"=>["命運石之門"], "KO"=>["슈타인즈 게이트"]}

    steins_gate.synopsis
     => ["Rintaro Okabe is a self-proclaimed "mad scientist" ... "]

    steins_gate.num_episodes
     => ["24"]

    steins_gate.vintage
     => ["2011-04-03 (Advanced screening)", "2011-04-05 to 2011-09-13"]

    steins_gate.genres
     => ["adventure", "comedy", "drama", "mystery", "psychological", "romance", "science fiction", "thriller"]

    steins_gate.themes
     => ["butterfly effect", "conspiracy", "technology", "Time travel"]

    steins_gate.op_theme
     => ["\"Hacking to the Gate\" by Kanako Ito"]

    steins_gate.ed_theme
     => ["\"Tokitsukasadoru Jūni no Meiyaku\" (刻司ル十二ノ盟約) by Yui Sakakibara", "#2: \"Sukai Kuraddo no Kansokusha\" (スカイクラッドの観測者) by Kanako Ito (ep 23)", "#3: \"Another Heaven\" by Kanako Itou (ep 24)"]


#####Cast and Staff:

    steins_gate.cast.find_all {|c| c.name.include? "Hanazawa"}
     => [#<struct ANN_Cast id="53741", role="Mayuri Shiina", name="Kana Hanazawa", lang="JA">]

    steins_gate.staff.find_all {|s| s.task.eql? "Director"}
     => [
            #<struct ANN_Staff id="593", task="Director", name="Takuya Satō">,
            #<struct ANN_Staff id="9693", task="Director", name="Hiroshi Hamasaki">,
            #<struct ANN_Staff id="35713", task="Director", name="Tomoki Kobayashi">
        ]


#####Episodes:

    steins_gate.episodes.find_all {|e| e.title.include? "Prologue"}
     => [
            #<struct ANN_Episode number="1", title="Prologue of the Beginning and End", lang="EN">,
            #<struct ANN_Episode number="24", title="The Prologue Begins With the End", lang="EN">
        ]

    steins_gate.episodes.first.to_h
     => {:number=>"1", :title=>"Prologue of the Beginning and End", :lang=>"EN"}

#####Images:

    steins_gate.images
     => [
            #<struct ANN_Image src="http://cdn.animenewsnetwork.com/thumbnails/fit200x200/encyc/A11770-1864351140.1370764886.jpg", width="200", height="125">,
            #<struct ANN_Image src="http://cdn.animenewsnetwork.com/thumbnails/max500x600/encyc/A11770-1864351140.1370764886.jpg", width="500", height="312">,
            #<struct ANN_Image src="http://cdn.animenewsnetwork.com/images/encyc/A11770-1864351140.1370764886.jpg", width="900", height="562">,
            #<struct ANN_Image src="http://cdn.animenewsnetwork.com/thumbnails/fit200x200/encyc/A11770-8.jpg", width="200", height="200">,
            #<struct ANN_Image src="http://cdn.animenewsnetwork.com/thumbnails/max500x600/encyc/A11770-8.jpg", width="317", height="317">
        ]
        
#####Ratings:

    steings_gate.ratings
     => [
            #<struct ANN_Rating votes="3788", weighted="9.1129", bayesian_score="9.1075">
        ]
        
###Fetch a manga:

Fetching a manga works exactly the same as an anime, but you should call the `fetch_manga` method.

    manga = ANN_Wrapper.fetch_manga "id"
    manga.title
    manga.alt_titles
    manga.synopsis
    manga.genres
    manga.vintage
    manga.themes
    manga.num_tankoubon
    manga.num_pages
    manga.id
    manga.type
    manga.staff
    manga.ratings
    manga.images
    manga.to_h

###Batching:
Send any number of ids in an array for a batch request.
This will return an array of ANN_Anime or ANN_Manga objects.

    anime = ANN_Wrapper.batch_anime(["id_1", "id_2", "id_3", ...])
    manga = ANN_Wrapper.batch_manga(["id_1", "id_2", "id_3", ...])

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
