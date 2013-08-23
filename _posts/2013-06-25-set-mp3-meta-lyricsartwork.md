---
layout: post
title: "set mp3 meta lyrics/artwork"
description: ""
category: perl
tags: ['perl', 'mp3']
---
{% include JB/setup %}

example code to set mp3 Lyrics and Artwork

	use MP3::Tag;

	open(my $fh, '<', 'artwork.png');
	my $image_data = do { local $/; <$fh>; };
	close($fh);

	my $mp3 = MP3::Tag->new('test.mp3');

	my $id3v2;
	$id3v2 = $mp3->{ID3v2} if exists $mp3->{ID3v2};
	$id3v2 ||= $mp3->new_tag("ID3v2");

	$id3v2->title('test');
	$id3v2->add_frame('TALB', 'Album title TEST'); # Album/Movie/Show title
	$id3v2->add_frame('TPE1', 'Artist name TEST'); # Lead performer(s)/Soloist(s)
	$id3v2->add_frame('TPE2', 'BLBALA Artist name'); # Band/orchestra/accompaniment

	$id3v2->add_frame('USLT', 0, 'eng', '', "test blabla\naaa CCCa DDD");
	$id3v2->add_frame('APIC', 0, 'image/png', chr(0), '', $image_data);

	$id3v2->write_tag();

some code borrowed from

 * [http://www.perlmonks.org/?node_id=896405](http://www.perlmonks.org/?node_id=896405)
 * [http://computer-programming-forum.com/53-perl/ac4f024ad4a9d284.htm](http://computer-programming-forum.com/53-perl/ac4f024ad4a9d284.htm)