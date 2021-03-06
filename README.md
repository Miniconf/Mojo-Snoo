# NAME

Mojo::Snoo - Mojo wrapper for the Reddit API

# DESCRIPTION

[Mojo::Snoo](https://metacpan.org/pod/Mojo::Snoo) is a Perl wrapper for the Reddit API which
relies heavily on the Mojo modules. [Mojo::Collection](https://metacpan.org/pod/Mojo::Collection)
was the initial inspiration for going the Mojo route.
Skip to [synopsis](https://metacpan.org/pod/Mojo::Snoo#SYNOPSIS) to see how
[Mojo::Snoo](https://metacpan.org/pod/Mojo::Snoo) can be great for one-liners, quick
scripts, and full-blown applications!

# SYNOPSIS

    use Mojo::Snoo;

    # OAuth ONLY. Reddit is deprecating cookie auth soon.
    my $snoo = Mojo::Snoo->new(
        username      => 'foobar',
        password      => 'very_secret',
        client_id     => 'oauth_client_id',
        client_secret => 'very_secret_oauth',
    );

    # upvote each post in /r/Perl (casing does not matter)
    $snoo->subreddit('Perl')->things->each(
        sub { $_->upvote }
    );

    # Don't want to login? That's fine.
    # You can stick to methods which don't require login.
    # Omitting auth details is nice for one-liners:

    # print names of moderators from /r/Perl
    Mojo::Snoo->new->subreddit('Perl')->mods->each( sub { say $_->name } );

    # or do the same via Mojo::Snoo::Subreddit
    Mojo::Snoo::Subreddit->new('Perl')->mods->each( sub { say $_->name } );

    # print title and author of each post (or "thing") from /r/Perl
    # returns 25 "hot" posts by default
    Mojo::Snoo::Subreddit->new('Perl')->things->each( sub { say $_->title, ' posted by ', $_->author } );

    # get only self posts
    @selfies = Mojo::Snoo::Subreddit->new('Perl')->things->grep( sub { $_->is_self } );

    # get the top 3 controversial posts ("things") on /r/AskReddit
    @things = Mojo::Snoo::Subreddit->new('Perl')->things_contro_all(3);

    # print past week's top video URLs from /r/videos
    Mojo::Snoo::Subreddit->new('Perl')->things_top_week->each( sub { say $_->url } );

    # print the /r/Perl subreddit description
    say Mojo::Snoo->new->subreddit('Perl')->about->description;

    # even fetch a subreddit's header image!
    say Mojo::Snoo->new->subreddit('Perl')->about->header_img;

# METHODS

## multireddit

Returns a [Mojo::Snoo::Multireddit](https://metacpan.org/pod/Mojo::Snoo::Multireddit) object.

## subreddit

Returns a [Mojo::Snoo::Subreddit](https://metacpan.org/pod/Mojo::Snoo::Subreddit) object.

## link

Returns a [Mojo::Snoo::Link](https://metacpan.org/pod/Mojo::Snoo::Link) object.

## comment

Returns a [Mojo::Snoo::Comment](https://metacpan.org/pod/Mojo::Snoo::Comment) object.

## user

Returns a [Mojo::Snoo::User](https://metacpan.org/pod/Mojo::Snoo::User) object.

# API DOCUMENTATION

Please see the official [Reddit API documentation](http://www.reddit.com/dev/api)
for more details regarding the usage of endpoints. For a better idea of how
OAuth works, see the [Quick Start](https://github.com/reddit/reddit/wiki/OAuth2-Quick-Start-Example)
and the [full documentation](https://github.com/reddit/reddit/wiki/OAuth2). There is
also a lot of useful information of the [redditdev subreddit](http://www.reddit.com/r/redditdev).

# LICENSE

The (two-clause) FreeBSD License. See LICENSE for details.
