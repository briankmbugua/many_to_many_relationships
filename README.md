# HOW TO START THIS PROJECT

```bash
# create a new virtual enviroment
$: python3 -m venv venv
# activate the enviroment
$: source venv/bin/activate
# install the depedencies
$: pip install Flask Flask-SQLAlchemy
# set the env variables
$: export FLASK_APP=app
$: export FLASK_ENV=development
# open the flask shell to create the database tables
$: flask shell
# once in flask shell import db, Post model and the Comment model and create the database tables using db.create_all() function
>>> from app import db, Post, Comment
>>> db.create_all()
>>> exit()

# then populate the database using the init_db.py program
$: python3 init_db.py
# run the development server
$: flask run
# if you go to the browser you will have the application running at the folowing URL:
$: http://127.0.0.1:5000/
```

# Many_to_many relationship
- add a database model that will represent the tags table
- link it with the existing posts table using an association table, which is a table that connects your two tables in a many_to_many relationship.
- A many_to_many relationship links two tables where each item in a table has many related items in the other table.
- In the association table, each post will reference its tags and each tag references the posts tagged with it.
 

 ## A simple table for blog posts
 | id    | content |
 |-------|---------|
 | 1     | a post on life and death|
 | 2     | a post on joy|

 # A table for tags
  | id    | content |
 |-------|---------|
 | 1     | life    |
 | 2     | death   |
 | 3     | joy

 let's say you want to tag a post on life and death with life and death tags,you could do this by adding a new row on the posts table like so

 | id    | content                 |tags                 |
 |-------|-------------------------|---------------------|
 | 1     | a post on life and death|        1,2          |
 | 2     | a post on joy           |                     |

This approach doesn't work, because each column should only have one value.If you have multiple values, basic operations such as adding and updating data become cumbersome and slow,Instead there should be a third table that references primary keys of related tables--this table is often called an association table or a join table and it stores IDs of each item from each table

### example of an association table that links between posts and tags
 | id    | post_id  |tag_id        |
 |-------|----------|--------------|
 | 1     | 1        |          1   |
 | 2     | 1        |          2   |

 In the first row, the post with the ID 1(that is, A post on life and death) relates to the tag with 1D 1(life), In the second row, the same post also relates to the tag with ID 2(death).This means that the post is tagged with both the life and death tags.Similarly, you can tag each post with multiple tags.