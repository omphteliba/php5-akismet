# Introduction

This is a simple little PHP7 class that enables you use the Akismet anti-spam service in your PHP7 application.

# Download

Check out the git repository:

	git clone git@github.com:omphteliba/php7-akismet.git

# Installation

Once you have cloned the repo (see Download, above) copy the file at src/main/php/net/omphteliba/Akismet.class.php to somewhere accessible to your scripts. Use include or a derivative to import it into your script.


# Documentation

See the [PHPDocs](http://achingbrain.github.com/maven-repo/documentation/php5-akismet/apidocs).

# Usage

Before you can use Akismet, you need a WordPress API key (they are free and getting one takes about five minutes). Once you have one, take a look at the code below:

	$WordPressAPIKey = 'aoeu1aoue';
	$MyBlogURL = 'http://www.example.com/blog/';
	
	$akismet = new Akismet($MyBlogURL ,$WordPressAPIKey);
	$akismet->setCommentAuthor($name);
	$akismet->setCommentAuthorEmail($email);
	$akismet->setCommentAuthorURL($url);
	$akismet->setCommentContent($comment);
	$akismet->setPermalink('http://www.example.com/blog/alex/someurl/');
	
	if($akismet->isCommentSpam())
	  // store the comment but mark it as spam (in case of a mis-diagnosis)
	else
	  // store the comment normally

That's just about it. In the event that the filter wrongly tags messages, you can at a later date create a new object and populate it from your database, overriding fields where necessary and then use the following two methods to train it:

	$akismet->submitSpam();

and

	$akismet->submitHam();

to submit mis-diagnosed spam and ham, which improves the system for everybody. See the included documentation for a complete run-down of all available methods.

## Changelog

### Version 0.1

Internal testing version, works with Akismet 3.1.7
