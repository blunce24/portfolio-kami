---
layout: post
title: BlocJams
thumbnail-path: "img/Landing.png"
short-description: BlocJams is a Spotify replica for playing your favorite music.

---

{:.center}
![]({{ site.baseurl }}/img/Landing.png)

## Explanation

For my first project, I set out to build [BlocJams](https://github.com/blunce24/bloc-jams-angular), a replica of Spotify, with the guidance of Bloc. The application was a vehicle to learn basic HTML and CSS, as well as front-end programming using vanilla JavaScript, jQuery, and AngularJS. I learned a lot through this process and encountered some interesting challenges.

## Problem

The first part of the project focused on building a foundation of HTML/CSS and JavaScript for both myself and the application. I wanted the app's style to be consistent with modern web applications, including having a responsive design. I used DOM scripting with JavaScript to make the app interactive. I then refactored the application with jQuery, introducing a music player with play/pause and seek functionality. The last step was to refactor the application with AngularJS, and further add play-on-page-load and mute capabilities.

## Solution

**HTML and CSS**

* I included the `normalize.css` file to ensure that all elements in the app were consistent with current standards.
* I utilized responsive web development methods, such as CSS media queries to apply styles based on device breakpoints:
{% highlight javascript %}
@media (min-width: 640px) {
	html { font-size: 112%; }

	.column {
		float: left; 	
		padding-left: 1rem;
		padding-right: 1rem;
	}

	.column.full { width: 100%; }
	.column.two-thirds { width: 66.7%; }
	.column.half { width: 50%; }
	.column.third { width: 33.3%; }
	.column.fourth { width: 25%; }
	.column.flow-opposite { float: right; }
}
{% endhighlight %}

**JavaScript and the DOM**

* I used event listeners to implement functionality such as toggling in album view:
{% highlight javascript %}
albumCover.addEventListener('click', function(event) {
	var albumTitle = document.getElementsByClassName('album-view-title')[0];
	if (albumTitle.firstChild.nodeValue === "The Colors") {
		setCurrentAlbum(albumMarconi);
	} else if (albumTitle.firstChild.nodeValue === "The Telephone") {
		setCurrentAlbum(albumEdison);
	} else if (albumTitle.firstChild.nodeValue === "The Lightbulb") {
		setCurrentAlbum(albumPicasso);
	}
});
{% endhighlight %}

* I constructed a `findParentByClassName` function that traversed the DOM upward to find a parent with the specified class. This function was then used to extend the play/pause character of the album view:
{% highlight javascript %}
var findParentByClassName = function(elem, targetClass) {
	for ( ; elem && elem !== document; elem = elem.parentNode) {
		if (elem.parentNode.className === targetClass) {
			return elem.parentNode;
		}
	}
};
{% endhighlight %}

**jQuery**

* I refactored the application using jQuery selectors and the jQuery API to handle events, animation, and document manipulation.
* I used jQuery to add a music player with play/pause and seek functionality:

{:.center}
![]({{ site.baseurl }}/img/playerBar.png)

**AngularJS**

* In addition to refactoring the application with the Angular framework, I extended the application's capabilities by implementing a play on load `init` function in the Album controller:
{% highlight javascript %}
(function() {
	function AlbumCtrl(Fixtures, SongPlayer) {
		this.albumData = Fixtures.getAlbum();
		this.songPlayer = SongPlayer;
		var init = function() {
			SongPlayer.play(Fixtures.getAlbum().songs[0]);
		};
		init();
	}
	angular
		.module('blocJams')
		.controller('AlbumCtrl', ['Fixtures', 'SongPlayer', AlbumCtrl]);
})();
{% endhighlight %}
* I also implemented a `toggleMute` function utilizing the [Buzz API](http://buzz.jaysalvat.com), which is applied to the volume icon in the player bar:
{% highlight html %}
<a class='icon' ng-click='playerBar.songPlayer.toggleMute()'>
	<span class='ion-volume-high'
    	ng-show='!playerBar.songPlayer.currentSong.muted'>
    </span>
    <span class='ion-volume-mute'
        ng-show='playerBar.songPlayer.currentSong.muted'>
	</span>
</a>
{% endhighlight %}

## Results

{:.center}
![]({{ site.baseurl }}/img/Collection.png)

Through JavaScript, the jQuery API, the Buzz API, and the AngularJS framework, I built a Spotify replica with the ability to display an album collection, as well as an individual album. It contains a song player that has play/pause, next/previous, and seek functionality. I gained experience in constructing algorithms to implement user stories, utilizing responsive web design, and refactoring code.

{:.center}
![]({{ site.baseurl }}/img/Album.png)

## Conclusion

Though there is functionality that BlocJams lacks, it was a rewarding first pass at front-end web development. I was able to see the connection between the code on the screen and the interactive aspects in the application. In addition, I was exposed to the AngularJS framework, and I have a better idea of what goes in to constructing a user-friendly, highly functional web application.
