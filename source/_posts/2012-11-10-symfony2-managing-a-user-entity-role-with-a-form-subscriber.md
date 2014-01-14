---
title: 'Symfony2: Managing a User entity role with a Form Event Subscriber'
author: Craig
layout: post
permalink: /2012/11/10/symfony2-managing-a-user-entity-role-with-a-form-subscriber/
categories:
  - PHP
  - Symfony2
---
I&#8217;m working on a Symfony2 application which makes use of roles to manage what Users of the system are able to do within the app. Symfony places no limit on the amount of roles the User can have, but in the context of my application, there are only two &#8211; a base user (ROLE\_USER, in Symfony parlance), and an administrator (ROLE\_ADMIN). As is Symfony custom, all users would possess the default role, but the administrator role would be granted on a per user basis. I&#8217;m using the FOSUserBundle and Doctrine, so a User&#8217;s roles are stored within an array on that User&#8217; Doctrine entity.

I began crafting a form (using the Symfony Form component) to manage user details. When creating forms that are bound to Doctrine I&#8217;ve generally found that I&#8217;ve needed to do little in the way of form customisation; the form component does a good job of figuring out which form fields to use based on the type of the variable it is given. So name, being a string, gets modelled as a textfield, while their registration date, being a DateTime object, causes a series of select boxes to be created which allow dates and times to be entered. So far so good.

But of course there has to be a reason for a blog post, and this is mine: I wanted a checkbox to toggle on/of the administrator role for each user. Since roles are stored in an array on the bound entity, the default is to render a collection of fields, which leads to an array of values being submitted by the form. Trying to modify the field definition to a &#8216;single&#8217; field, like a checkbox, led to an error as the Form component doesn&#8217;t know how to map an array to a single value. A multi-value field wasn&#8217;t an option as I didn&#8217;t want to expose the roles (which wouldn&#8217;t necessarily make sense to an end user), and I didn&#8217;t want to get into messing about with Twig templates if I could help it; a bit of Googling led me to [this article][1] on the cookbook, which describes how to dynamically add elements to forms using a Form event subscriber; this turned out to be just what I needed.

Reading through the cookbook article, the following plan took shape: when the form is created, add a checkbox to the form which is ticked depending on whether the User object bound to the form has the administrator role. When the form is submitted, if the checkbox is ticked, grant the user that role. If it is not, remove the role from their array of granted roles.

[<img class="aligncenter size-full wp-image-311" title="The resulting form" src="/images/posts/2012/11/Screen-Shot-2012-11-10-at-14.51.51.png" alt="" width="793" height="491" />][2]

To implement this, I needed two classes; a Form class, of course, and a new class that implements Symfony\Component\EventDispatcher\EventSubscriberInterface and subscribes to events on the form. As in the cookbook example, when the &#8216;preSetData&#8217; event fires I&#8217;d be adding a field to the form. In addition, when the &#8216;bind&#8217; event fires, I&#8217;d be using the value of the field to modify the bound object, in this case the User being managed. This is what I ended up with:

<noscript>
  <p>
    View the code on <a href="https://gist.github.com/4051034">Gist</a>.
  </p>
</noscript>

I&#8217;m manually adding the subscriber to the form in UserType::buildForm(), which feels a bit weird when the usual approach would be to define a service and tag it appropriately. I&#8217;m not sure if that&#8217;s possible with Form subscribers, that&#8217;s just how the cookbook approach went. I&#8217;d imagine there are other ways I could have achieved the same result, but I like this approach because I don&#8217;t have to modify my User class at all, and I don&#8217;t have to delve into form field customisation.

The only downside I&#8217;ve found so far is that there doesn&#8217;t seem to be a way to order the fields that get added in the listener &#8211; they are always placed at the start of the collection, regardless of when the subscriber is attached to the form. This means that some template work is necessary to place the field as desired.

 [1]: http://symfony.com/doc/current/cookbook/form/dynamic_form_generation.html
 [2]: /images/posts/2012/11/Screen-Shot-2012-11-10-at-14.51.51.png