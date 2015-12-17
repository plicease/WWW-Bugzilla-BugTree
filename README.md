# WWW::Bugzilla::BugTree [![Build Status](https://secure.travis-ci.org/plicease/WWW-Bugzilla-BugTree.png)](http://travis-ci.org/plicease/WWW-Bugzilla-BugTree)

Fetch a tree of bugzilla bugs blocking a bug

# SYNOPSIS

    use WWW::Bugzilla::BugTree;
    
    my $tree = WWW::Bugzilla::BugTree->new(
      url => 'http://bugzilla',
    );
    
    # $bug isa WWW::Bugzilla::BugTree::Bug
    my $bug = $tree->fetch(749922);
    print $bug;
    foreach my $subbug (@{ $bug->children })
    {
      print $bug;
    }

# DESCRIPTION

This module provides a way to fetch a tree of dependent bugs from Bugzilla.
You give it a bug id and it returns a tree of all the bugs that bug depends
on (or all the bugs that are blocking your bug).  I wrote this to use the
`XML` output of Bugzilla's `show_bug.cgi` page because we are still using
Bugzilla 3.6, which doesn't provide dependency information via its API, which
would probably be faster.

There is also a companion script [bug\_tree](https://metacpan.org/pod/bug_tree) which will print out the tree
for you with pretty colors indicating each bug's status.

# ATTRIBUTES

## ua

    my $lwp = $tree->ua;

Instance of [LWP::UserAgent](https://metacpan.org/pod/LWP::UserAgent) used to fetch information from the
bugzilla server.

## url

    my$url = $tree->url

The URI of the bugzilla server.  You may pass in to the constructor
either a string or a [URI](https://metacpan.org/pod/URI) object.  If you use a string it will
be converted into a [URI](https://metacpan.org/pod/URI).

If not provided it falls back to using the `BUG_TREE_URL` environment
variable, and if that isn't set it uses this bugzilla provided for
testing:

[Bugzilla v4.2](https://landfill.bugzilla.org/bugzilla-4.2-branch)

# METHODS

## fetch

    my $bug = $tree->fetch($id);

Fetch the bug tree for the bug specified by the given `id`.  Returns
an instance of [WWW::Bugzilla::BugTree::Bug](https://metacpan.org/pod/WWW::Bugzilla::BugTree::Bug).

## clear\_cache

    $tree->clear_cache;

Clears out the cache.

# SEE ALSO

[bug\_tree](https://metacpan.org/pod/bug_tree), [WWW::Bugzilla::BugTree::Bug](https://metacpan.org/pod/WWW::Bugzilla::BugTree::Bug)

# AUTHOR

Graham Ollis &lt;plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2013 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
