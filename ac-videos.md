---

copyright:
  years: 2021
lastupdated: "2021-01-19"

keywords: app-configuration, app configuration, sample apps

subcollection: app-configuration

---

{:codeblock: .codeblock}
{:external: target="_blank" .external}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:download: .download}
{:script: data-hd-video='script'}
{:video: .video}

# Videos
{: #ac-videos}

You can watch the videos to learn more about {{site.data.keyword.appconfig_short}} service.
{: shortdesc}

![What are Feature Flags?](https://www.youtube.com/embed/AJa2B-twtG4){: video output="iframe" data-script="#feature-flags-concept-transcript" id="youtubeplayer" width="560" height="315" scrolling="no" allowfullscreen webkitallowfullscreen mozAllowFullScreen frameborder="0" style="border: 0 none transparent;"}

## Video transcript
{: #feature-flags-concept-transcript}
{: notoc}

What are Feature Flags?

Before you begin playing the video: In this video, the narrator draws representational images on the display board to explain the concept. [Draw] is used to represent when the narrator draws the representational image. [Writing] is used to represent when the narrator writes some text.

What if you could release a feature to different groups of users without deployment?
Is there a way to effectively test features in production, and immediately roll them back if needed?

Hi, my name is Dilan Orrino with IBM Cloud. I'll be answering those questions by discussing feature flags, or sometimes referred to as feature toggle, or switches. 

Feature flags are conditions that encompass feature code that allow you to flip them on and off at will. 
Okay, let's use an example. 
[Draw] Let's say we've got an ice cream shop franchise that's looking to expand to a new city and we've got a 
[Draw] banner that we want to display on our website. We'll call this open banner.
We only want to display this banner to users that are [Draw] nearby our new ice cream shop we can do this by using feature flags. 

There's a couple benefits to using feature flags. 
[Writing] Number one is we can actually turn these on or off without deployment.
[Writing] Number two is we can actually test directly in production.
[Writing] And number three we can segment our users based on different attributes.

Okay, there's a couple ways you can do this one way is by using properties in JSON files or config maps. There's a better way however by using a feature flag service. 

[Writing] There's a couple benefits to using a feature flag service. Number one is you can have essentially managed place for your features, or excuse me your feature flags. 
[Writing] Number two is you can turn these on and off  without modifying your properties in your future, in your apps or web pages. 
[Writing] And number three is you get audit and usage data. It's harder to get the audit and usage data by using JSON files.

Okay, so now let's go back to our example we've got our open banner feature and now let's wrap it with some feature flag code. 

And so here's an example, kind of pseudo code, that you can use if store open is enabled.

[Writing] if (storeopen is Enabled()){ 
Then we're going to show open banner    
[Writing] show Open Banner();} 

so this pseudocode represents our feature code and the flag that potentially could encompass it. 

Now let's actually put this in production and [Draw] make it show showcase to some users. 

So now that we've got our feature in production it's not usable to any users right now this is an idea typically displayed with feature flags called dark launch. Dark launch is when a feature is in production but not visible to any or all users or any or some users, excuse me.

Now we want to introduce the idea of [Writing] segments. 

So we've already said that we only want a certain number of people to view this, people who are nearby our new shop. This will be our segment A, and a segment is simply users or groups of users that have attributes tied to them. 

So this first one might have [Writing] current location, and [Writing] zip code.

Attributes, this allows users who are either currently in the location or have already stipulated that they live nearby to view this feature, but before we do that we want to test the feature out on our own employees. [Writing] So we would have segment Bof our testers because we want them to be our employees the attribute might be [Writing] email ID.

Now we can effectively test our feature in production by {Draw] flipping this toggle on. So now this feature is on for our testers, and say maybe something went wrong so we're actually going to flip it off fix it, and then we'll turn it back on for segment B.

Once we're satisfied that everything is working well. Then we can flip this on for our [Draw] segment A.

Now all this is done without a deployment because our feature is already in production. All we're doing is making it visible or not visible to certain users.

Once it is in production. [Draw] We can actually add a little bit of automation to this 

with our testers, we did it manually, we flipped it on and off manually, but with feature flags we can actually add a time element. So let's say we only want this to be viewable for [Writing] three weeks, 

two weeks before grand opening, one week after grand opening of our new shop. This will be flipped on and then automatically turned off or not visible for this segment of users after three weeks. 

Okay, so now we're getting really good at using feature flags so our [Draw] feature flags are potentially starting to stack up we might have a couple apps and a couple websites with a couple different types of features that are flagged. 

So we've got maybe [Writing] app one here, [Writing] app two, and say a [Writing] web page.

With a feature flagging service we can actually group these in collections so that we're a little bit more organized with which feature flags are tied to, which apps are web pages. 

So now today we've learned about returning feature flags on and off without deployment testing directly in production, and then segmenting those features based on the user attributes. 

Thank you for watching. If you have questions, please drop us a line below. If you want to see more videos like this in the future, please like and subscribe. And don't forget, you can grow your skills and earn badges with IBM CloudLabs, which are free browser-based interactive kubernetes labs. 
