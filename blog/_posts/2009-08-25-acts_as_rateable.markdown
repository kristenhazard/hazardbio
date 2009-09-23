---

layout: post
title: Step by step guide to implementing acts_as_rateable into your rails application
topics: rails 
published: true
excerpt: Here is a step by step guideline to implement as_as_rateable plugin into your rails application...

---

Here are the steps described for a beginner:

###Part 1: get plugin installed, add  and make a single model as_as_rateable
1. Run `script/plugin install git://github.com/azabaj/acts_as_rateable.git` in terminal at root of your application
2. Run `script/generate acts_as_rateable_migration` in terminal at root of your application
3. Run `rake db:migrate` in terminal at root of your application
4. Add `acts_as_rateable` to my the model that you want to rate
5. Restart `script/server`
6. Start `script/console` to test basic acts_as_rateable methods to prove installation was successful

###At this point the best way to test the installation, migration and acts_as_rateable in my opinion would be to go the console:
Create an item object to rate

    >> item = Item.find_by_id(6)
    => #<Item id: 6, title: "March", itemtype: "Book", author: "Geraldine Brooks", 
    description: "  From Louisa May Alcott’s beloved classic <I>Lit...", 
    asin: "0143036661", detailpageurl: "http://www.amazon.com/March-Geraldine-Brooks/dp/014...", 
    smallimageurl: "http://ecx.images-amazon.com/images/I/51K4CPKPJSL._...", 
    mediumimageurl: "http://ecx.images-amazon.com/images/I/51K4CPKPJSL._...", 
    publicationdate: "2006-01-31", created_at: "2009-05-29 22:58:14", 
    updated_at: "2009-05-29 22:58:14">

Create a current user object

    >> current_user = User.find_by_id(1)
    => #<User id: 1, username: "kristen1", email: "kristen@hazardbio.com", 
    crypted_password: "3342ac0ad4dd89e53ebcdee115cb99764a43f7c058a2ec2e56e...", 
    password_salt: "I3V0HfUl6jrebbOCzpoa", 
    persistence_token: "5a9dff09cce526cfe6d7abd80c789edca5c86eed9ccab630436...", 
    login_count: 13, failed_login_count: 0, last_request_at: "2009-08-25 20:56:45", 
    current_login_at: "2009-08-25 18:41:02", last_login_at: "2009-08-18 16:46:06", 
    current_login_ip: "127.0.0.1", last_login_ip: "127.0.0.1", 
    created_at: "2009-08-06 22:15:34", updated_at: "2009-08-25 20:56:45">
  
Test method rate_it using item and current_user.id 

    >> item.rate_it(5,current_user.id)
    => true


###Part 2: get ratings working in the view

http://www.komodomedia.com/blog/2007/01/css-star-rating-redux/
http://blog.aisleten.com/2007/05/03/ajax-css-star-rating-with-acts_as_rateable/
http://swik.net/Rails/Dave+Naffis+-+Rails,+Ruby,+Randomness/Ruby+on+Rails,+Ajax+&+CSS+Star+Rating+System/kqn0