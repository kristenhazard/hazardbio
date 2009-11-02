---

layout: post
title: Step by step guide to implementing acts_as_rateable into your rails application - part 2
topics: rails 
published: true
excerpt: Here is a step by step guideline to implement as_as_rateable plugin into your rails application...part 2

---

###Part 2: get ratings working in the view

###Create RatingsController

I can't remember if running acts_as_rateable_migration created a RatingsController for you or not, if it did not go ahead and create one now.

    class RatingsController < ApplicationController
      before_filter :require_user
      def rate
        @asset = Item.find(params[:id])
        Rating.delete_all(["rateable_type = 'Item' AND rateable_id = ? AND user_id = ?", @asset.id, current_user.id])
        @asset.rate_it(params[:rating], current_user.id)
        render :update do |page|
          page.replace_html 'star-ratings-block', :partial => 'ratings/rating', :locals => { :asset => @asset }
          page.visual_effect :highlight, 'rate'
        end
      end
    end

I simplified my ratings controller by hardcoding 'Item' as the rateable_type. 
Since acts_as_rateable is polymorphic you don't need to hardcode the rateable_type. Here is a 
[write up](http://blog.aisleten.com/2007/05/03/ajax-css-star-rating-with-acts_as_rateable/) that shows 
how to create a controller that utilizes the polymorphic nature of acts_as_rateable.  See step 4.


###Create a partial to receive rating from user

Partial

    <ul class='star-rating'>
      <% unless asset.rating(current_user).nil? %>
        <li class='current-rating' style='width:<%= (asset.rating(current_user) * 25).to_i -%>px;'>
        </li>
      <% end %>
        <li>
            <%= link_to_remote( "1", {:url => { :controller => "ratings", 
                :action => "rate", :id => asset.id, :rating => 1}},
                :class => 'one-star', :name => '1 star out of 5') %>
        </li>
        <li>
            <%= link_to_remote( "2", {:url => { :controller => "ratings", 
                :action => "rate", :id => asset.id, :rating => 2}},
                :class => 'two-stars', :name => '2 stars out of 5') %>    
        </li>
        <li>
            <%= link_to_remote( "3", {:url => { :controller => "ratings", 
                :action => "rate", :id => asset.id, :rating => 3}},
                :class => 'three-stars', :name => '3 stars out of 5') %>
        </li>
        <li>
            <%= link_to_remote( "4", {:url => { :controller => "ratings", 
                :action => "rate", :id => asset.id, :rating => 4}},
                :class => 'four-stars', :name => '4 stars out of 5') %>    
        </li>
        <li>
            <%= link_to_remote( "5", {:url => { :controller => "ratings", 
                :action => "rate", :id => asset.id, :rating => 5}},
                :class => 'five-stars', :name => '5 stars out of 5') %>
        </li>
    </ul>

Calling partial in view

    <div id="star-ratings-block">
      <%= render :partial => "ratings/rating", :locals => { :asset => @item } %>
    </div>

###Create a partial to show average ratings

Partial

    <ul class='star-rating'>
        <li class='current-rating' style='width:<%= (asset.average_rating * 25).to_i -%>px;'></li>
    </ul>
    <div class="num-ratings">
      (<%= asset.rates.size %>)
    </div>
    
Calling partial in view

    <div id="avg-rating">
      <%= render :partial => "ratings/avg_rating", :locals => { :asset => @item } %>
    </div>
    

###[Check out my implementation](http://times-arrow.com/timelines/1)
You have to be logged in to rate books at this site. Sign up and check it out.

###These write ups were very helpful.

[For css and gif files](http://www.komodomedia.com/blog/2007/01/css-star-rating-redux/)

[Great step by step guide](http://blog.aisleten.com/2007/05/03/ajax-css-star-rating-with-acts_as_rateable/)

[Another step by step guide](http://swik.net/Rails/Dave+Naffis+-+Rails,+Ruby,+Randomness/Ruby+on+Rails,+Ajax+&+CSS+Star+Rating+System/kqn0)