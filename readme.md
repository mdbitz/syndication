# Content Syndication #

[VIP Documentation](https://vip.wordpress.com/plugins/syndication/)

Syndication allows you to "push" content to multiple WordPres sites or pull content from external sites (WordPress, 
RSS Feeds, etc).

## How it Works ##

### Register and Group Sites ###

* Register the sites/feed that you want to push/pull content from under "Sites"
* Group Sites into sitegroups to easily manage common syndications

### Configure Syndicated Content ###

* Specify Post Types that support push syndication
* Per Pull Site configure Post Types to be pulled

### Syndicate Content ###

* When publishing or updating content select sitegroups within the "Syndication" metabox that the content should be syndicated 
(pushed) to.

## Available Filters & Actions ##

When Syndicating content you might want to have various functions triggered when new content is published on your site 
or externally. The following additional filters/actions are available to enable additional logging, content 
modifications, or other needs. As a note when publishing content to external sites (push) no new hooks are available 
and instead you would need to utilize `save_post` or other core hooks.  

In addition to the general hooks detailed below each Transport method has filters/actions available to further modify 
the data pulled into this site or pushed to an external site.

### Push Syndication ###
* **syn_pre_push_post_sites** <br/>
    Filter the sites the content (post) should be syndicated to (push) <br/><br/>
    `$sites = apply_filters( 'syn_pre_push_post_sites', $sites, $post_ID, $slave_post_states );`
    
* **syn_pre_push_new_post_shortcircuit** <br/>
    Filter to shortcircuit publication of content to an external site <br/><br/>
    `$push_new_shortcircuit = apply_filters( 'syn_pre_push_new_post_shortcircuit', false, $post_ID, $site, $transport_type, $client, $info );` 
    
* **syn_post_push_new_post** <br/>
    Action to be performed after post has been published to an external site.<br/><br/>
    `do_action( 'syn_post_push_new_post', $result, $post_ID, $site, $transport_type, $client, $info );`
  					
* **syn_pre_push_edit_post_shortcircuit** <br/>
    Filter to shortcircuit updating content to an external site <br/><br/>
    `$push_edit_shortcircuit = apply_filters( 'syn_pre_push_edit_post_shortcircuit', false, $post_ID, $site, $transport_type, $client, $info );` 
    
* **syn_post_push_edit_post** <br/>
    Action to be performed after post has been updated on an external site.<br/><br/>
    `do_action( 'syn_post_push_edit_post', $result, $post_ID, $site, $transport_type, $client, $info );`
  	
* **syn_pre_push_delete_post_shortcircuit** <br/>
    Filter to shortcircuit deleting of content to an external site <br/><br/>
    `$push_delete_shortcircuit = apply_filters( 'syn_pre_push_delete_post_shortcircuit', false, $post_ID, $site, $transport_type, $client, $info );` 
    
* **syn_post_push_delete_post** <br/>
    Action to be performed after post has been deleted on an external site.<br/><br/>
    `do_action( 'syn_post_push_delete_post', $result, $post_ID, $site, $transport_type, $client, $info );`
  	
### Pull Syndication ###
* **syn_pre_pull_posts** <br/>
    Filter posts that are to be pulled (published/updated) on this site.<br/><br/>
    `$posts          = apply_filters( 'syn_pre_pull_posts', $client->get_posts(), $site, $client );`
    
* **syn_pre_pull_edit_post_shortcircuit** <br/>
    Filter to shortcircuit updating of content pulled to this site <br/><br/>
    `$pull_edit_shortcircuit = apply_filters( 'syn_pre_pull_edit_post_shortcircuit', false, $post, $site, $transport_type, $client );`

* **syn_pull_edit_post** <br/>
    Filter to modify post before it is updated on this site <br/><br/>
    `$post = apply_filters( 'syn_pull_edit_post', $post, $site, $client );`
    
* **syn_post_pull_edit_post** <br/>
    Action to be performed after post has been updated on this site.<br/><br/>
    `do_action( 'syn_post_pull_edit_post', $result, $post, $site, $transport_type, $client );`

* **syn_pre_pull_new_post_shortcircuit** <br/>
    Filter to shortcircuit publishing of new content pulled to this site <br/><br/>
    `$pull_new_shortcircuit = apply_filters( 'syn_pre_pull_new_post_shortcircuit', false, $post, $site, $transport_type, $client );`

* **syn_pull_new_post** <br/>
    Filter to modify new post before it is pulled to this site <br/><br/>
    `$post = apply_filters( 'syn_pull_new_post', $post, $site, $client );`
    
* **syn_post_pull_new_post** <br/>
    Action to be performed after new post has been pulled to this site.<br/><br/>
    `do_action( 'syn_post_pull_new_post', $result, $post, $site, $transport_type, $client );`

### Misc ###
* **syn_pre_find_post_by_guid** <br/>
    Filter to obtain `post_id` on this site if meta is modified.<br/><br/>
    `$post_id = apply_filters( 'syn_pre_find_post_by_guid', false, $guid, $post, $site );`

### CLI Commands ###
If needed users can utilize wp-cli commands to trigger syndication of content (push and pull).

```
$ wp syndication
usage: wp syndication push-all-posts [--post_type=<post-type>] [--paged=<page>]
   or: wp syndication push_post --post_id=<post-id>
   or: wp syndication pull_site --site_id=<site-id>
   or: wp syndication pull-sitegroup --sitegroup=<sitegroup>
```

## Contributing ##


If you are interested in contributing, we need help with two main areas:

1. Fixing bugs in v1
2. Feature development in v2

Issues have been created for each of the planned feature developments. Help with documentation for both versions is also greatly appreciated.
