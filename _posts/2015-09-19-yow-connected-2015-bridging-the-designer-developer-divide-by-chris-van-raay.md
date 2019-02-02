---
id: 1465
title: 'YOW! Connected 2015: Bridging the Designer &#8211; Developer Divide by Chris van Raay'
date: 2015-09-19T18:08:49+00:00
author: deline
layout: post
guid: http://delineneo.com/?p=1465
permalink: /2015/09/yow-connected-2015-bridging-the-designer-developer-divide-by-chris-van-raay/
categories:
  - Programming
  - Technology
---
I had the opportunity to go down to Melbourne for the YOW! Connected 2015 conference. It&#8217;s the second YOW! Connected to be held and even though it was at a smaller venue this year I enjoyed it just as much as last year.

What I enjoy about conferences is it&#8217;s a chance to hear how other people are doing things, get interesting insights and things to look into. And lastly to somewhat reassure you that as a developer (and organisation) the decisions you&#8217;ve made so far have actually been sensible choices. When you&#8217;re sitting in an audience and multiple speakers are mentioning things along the same lines there definitely is a sense of relief in a way.

But back to the conference. Whilst the conference covered both mobile development and the IoT, I mainly attended talks leaning on the mobile development side. For me there were two running themes in this space:

  * Designers and developers working together
  * The use of reactive programming in mobile development

There were also a few talks on mobile app testing, CI and CD that reaffirmed for me the state of testing for mobile, the decision we&#8217;ve made so far and where we can go next.

I&#8217;ll focus on trying to get up my notes on the designer and developer talks first as there were 3-4 talks on this topic. Whilst every talk had differing ideas on how designers and developers could work better together the crux of it all was communication and having a shared understanding.

## Bridging the Designer &#8211; Developer Divide &#8211; [<span style="font-family: 'Helvetica Neue'; font-size: 10.5pt;">@chrisvanraay</span>](http://twitter.com/chrisvanraay)

#### Common issues in the divide

Chris opened by discussing a number of issues in the designer &#8211; developer divide and how they may be overcome:

**Us and them mentality
  
** <span style="line-height: 1.5;">Developers thinking &#8216;designers don&#8217;t know anything&#8217; and designers thinking &#8216;developers are lazy. To help overcome this:</span>

  * Designers should be experts in the platform they are designing for
  * Developers need to be honest. Nothing is impossible, just harder/hard to do.
  * Break down the walls and have respect for each other. Working in a cross functional team helps with this

**Implications of design decisions**
  
It&#8217;s not easy for designers to know what is easy/hard. You get get through this by simply talking and working through it together.

_Point 1 in &#8216;Us and them mentality&#8217; about being an expert will help in understanding the implications._

**Speaking different languages
  
** Designers and developers often speak in different terminology. Use a shared language. E.g. things you can standardise:

  * Are you talking pixels or points
  * Is it a screen or a view controller

**Design isn&#8217;t always measurable**
  
Developers need to understand design isn&#8217;t scientific and will have to be more patient.

**Geographical separation**
  
Easily overcome by co-locating/sit together. Also better handover docs (this is more relevant if you&#8217;re geographically separated).

**PSDs are terrible docs for developers to use**
  
These are often provided as the output of design for developers to use. They&#8217;re not ideal though as developers often don&#8217;t have Photoshop nor the skills to use it well. Designers could help developers learn enough Photoshop but PSD files aren&#8217;t valuable enough in itself.

**Conflict isn&#8217;t a bad thing
  
** It gives you a different view on things. But you both need to be able to compromise on things.

But at the end of the day designers and developers aren&#8217;t really that different. Your goals are really the same thing, just in a different language.

##### How/what can designers developers do to help bridge the divide?

How does a team overcome the issues identified above? There are a number of things that a team can do:

**Have a consistent design**
  
This means you have less things to build, as a common understand is shared between both parties. To achieve this there are obviously some changes/improvements that need to be made:

**Designers can structure their work to make the transition as painless as possible**

  * Communicate the design rationale
  * Documentation of the stuff you will look at every day. Things like font, spacing, colour palette
  * Use smarter prototyping tools
  * Handover a spec &#8211; if you&#8217;ve documented the common things, you can get down to just handing over a wireframe with the styles listed next to boxes.

**Developers can do the following things better**

  1. Code for consistency
  2. Code for change &#8211; Change is inevitable. Branding can change, apps get sold. Really this is the same as principle 1.

**But how can we do all this?
  
** A number of approaches we&#8217;re given on how designers and developers could help achieve the above:

  * Name your colours something easily understood. E.g. instead of saying &#8216;colour #8cd8fd&#8217;, maybe your team will call that colour SkyBlue.
  * Centralise colours &#8211; e.g. use a category to add your defined colours to UIColor.
  * Name your different font variations. E.g. H1 could be 17 point System Font.
  * Give names to combinations of fonts and styles so they can be references in wireframes. E.g. H1SkyBlue would mean the font is 17 point System Font in SkyBlue.
  * Document reusable views somewhere. This makes it easier for developers and designers to know what something looks like and refer to where it is already being used.

##### Why should we care about this all?

Everyone wants and loves working in a high functioning team. Happy designers + happy developers = a better functioning team. You&#8217;ll have increased flexibility and productivity and a general better working environment.

It was interesting listening to this talk as we&#8217;ve started doing some of the things mentioned above at work and the designers and developers already agree it is a better experience for both parties.

##### **Is bridging the divide an easy thing to do?**

Yes and no. You&#8217;ll need discipline and ensure designers and developers have both bought into the process. Things can get into the way like really strict rules on checking in code. All of these can be overcome if the team is willing to be flexible and do a bit of forward planning and creative allocation of work. E.g. if you&#8217;ve got a hefty design piece, split it down and sequence the stories in a ordered known way that makes sense. We&#8217;ve actually already started doing this at work and it&#8217;s been a much more pleasant process in getting design improvements delivered.

&nbsp;

&nbsp;