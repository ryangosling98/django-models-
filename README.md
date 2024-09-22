Create Table (Model)
To create a model, navigate to the models.py file in the /members/ folder.

Open it, and add a Member table by creating a Member class, and describe the table fields in it:

from django.db import models

class Member(models.Model):
  firstname = models.CharField(max_length=255)
  lastname = models.CharField(max_length=255)

The first field, firstname, is a Text field, and will contain the first name of the members.

The second field, lastname, is also a Text field, with the member's last name.

Both firstname and lastname is set up to have a maximum of 255 characters.



Now when we have described a Model in the models.py file, we must run a command to actually create the table in the database.

Navigate to the /my_tennis_club/ folder and run this command:


Django Insert Data
Add Records
The Members table created in the previous chapter is empty.

We will use the Python interpreter (Python shell) to add some members to it.

To open a Python shell, type this command:

py manage.py shell

At the bottom, after the three >>> write the following:

>>> from members.models import Member
>>> Hit [enter] and write this to look at the empty Member table:

>>> Member.objects.all()
>>> This should give you an empty QuerySet object, like this:

<QuerySet []>
A QuerySet is a collection of data from a database.

Read more about QuerySets in the Django QuerySet chapter.

Add a record to the table, by executing these two lines:

>>> member = Member(firstname='Emil', lastname='Refsnes')
>>> member.save()
>>>
>>> Execute this command to see if the Member table got a member:

>>> Member.objects.all().values()
Hopefully, the result will look like this:

<QuerySet [{'id': 1, 'firstname': 'Emil', 'lastname': 'Refsnes'}]>


Add Multiple Records
You can add multiple records by making a list of Member objects, and execute .save() on each entry:



member1 = Member(firstname='Tobias', lastname='Refsnes')
>>> member2 = Member(firstname='Linus', lastname='Refsnes')
>>> member3 = Member(firstname='Lene', lastname='Refsnes')
>>> member4 = Member(firstname='Stale', lastname='Refsnes')
>>> member5 = Member(firstname='Jane', lastname='Doe')
>>> members_list = [member1, member2, member3, member4, member5]
>>> for x in members_list:
>>>   x.save()

py manage.py makemigrations members

Now there are 6 members in the Member table:

>>> Member.objects.all().values()
<QuerySet [{'id': 1, 'firstname': 'Emil', 'lastname': 'Refsnes'},
{'id': 2, 'firstname': 'Tobias', 'lastname': 'Refsnes'},
{'id': 3, 'firstname': 'Linus', 'lastname': 'Refsnes'},
{'id': 4, 'firstname': 'Lene', 'lastname': 'Refsnes'},
{'id': 5, 'firstname': 'Stale', 'lastname': 'Refsnes'},
{'id': 6, 'firstname': 'Jane', 'lastname': 'Doe'}]>
>>
>>Django Update Data
Update Records
To update records that are already in the database, we first have to get the record we want to update:

>>> from members.models import Member
>>> x = Member.objects.all()[4]
>>>
>>> x will now represent the member at index 4, which is "Stale Refsnes", but to make sure, let us see if that is correct:

>>> x.firstname
This should give you this result:

'Stale'
Now we can change the values of this record:

>>> x.firstname = "Stalikken"
>>> x.save()
Execute this command to see if the Member table got updated:

>>> Member.objects.all().values()
Hopefully, the result will look like this:

<QuerySet [{'id': 1, 'firstname': 'Emil', 'lastname': 'Refsnes'},
{'id': 2, 'firstname': 'Tobias', 'lastname': 'Refsnes'},
{'id': 3, 'firstname': 'Linus', 'lastname': 'Refsnes'},
{'id': 4, 'firstname': 'Lene', 'lastname': 'Refsnes'},
{'id': 5, 'firstname': 'Stalikken', 'lastname': 'Refsnes'},
{'id': 6, 'firstname': 'Jane', 'lastname': 'Doe'}]>
