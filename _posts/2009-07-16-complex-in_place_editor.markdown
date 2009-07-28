---

layout: post
title: Rails complex in_place_editor implementation
topics: rails in_place_editor

---

Today I implemented Rails in_place_editor. The basic steps are:

1. install plugin
2. add in_place_edit_for to controller
3. add in_place_editor_field to view

My implementation was a little more complex because I was in place editing a field within the context of a different model. 
I was in place editing a field from my timeline_items model, within the view for my timeline model. 
Thus when I implemented in_place_editor_field per the standard documentation I received the following error:

###Error: ActionController::UnknownAction (No action responded to set_timeline_item_position_desc. Actions: add_item, create, destroy, edit, index, new, select_item, show, sort, and update):

Rails was looking for the method set_timeline_item_position_desc in my timeline controller, but that method was in my timeline_item controller. (It was automatically created by Rails in my timeline controller due to the line in_place_edit_for :timeline_item, :position_desc)

The solution was to add a couple of things to the in_place_editor field:

1. @timeline_item = timelineitem;
2. :url => { :controller => 'timeline_items', :action => 'set_timeline_item_position_desc', :id => timelineitem.id }

###Summary

Install plugin: 

`$ script/plugin install git://github.com/rails/in_place_editing.git`

Controller: 

`in_place_edit_for :timeline_item, :position_desc`

View:

`<%= @timeline_item = timelineitem; in_place_editor_field :timeline_item, :position_desc, {}, :url => { :controller => 'timeline_items', :action => 'set_timeline_item_position_desc', :id => timelineitem.id }, :cols => 5 %>`
                                           


These 2 posts pointed my in the right direction:

This first one described why I needed to add the following: @timeline_item = timelineitem

[http://weeatbricks.com/2007/09/01/in_place_editor_field-method-in-ruby-on-rails/]
(http://weeatbricks.com/2007/09/01/in_place_editor_field-method-in-ruby-on-rails/)


This second one described why I need to add the following: :url => { :controller => 'timeline_items', :action => 'set_timeline_item_position_desc', :id => timelineitem.id }


[http://www.postal-code.com/binarycode/2007/04/13/in_place_edit_for-in_place_editor_field-and-complex-cases/]
(http://www.postal-code.com/binarycode/2007/04/13/in_place_edit_for-in_place_editor_field-and-complex-cases/)
