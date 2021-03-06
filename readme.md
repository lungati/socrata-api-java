The Socrata Java API
====================

So you like transparency. You're like the glass window of government agencies. You're like the invisible man of public servants.

HOWEVER...

It sure would be nice if someone could provide an API for publishing and accessing your agency's data on their socrata platform.

_Booyakasha!_
=============

Example (Everyone loves examples)
=================================

Creating a dataset
------------------

    Connection c = new HttpConnection("robots.dod.gov", "sam.gibson@socrata.com", "******", "******");
    View v = new View();
    v.setName("Robotic Attack Units by Year");
    v.setDescription("Seriously? You need more of a description than that?");
    View.Column unit = new View.Column();
    unit.setName("Unit");
    unit.setDataTypeName("text");

    View.Column year = new View.Column();
    year.setName("Year");
    year.setDataTypeName("number");

    v.addColumn(unit);
    v.addColumn(year);

    v.create(c);

Importing a file into a dataset
-------------------------------

    // Setup the view with the columns that you want
    // [...]
    Connection c = new HttpConnection("robots.dod.gov", "sam.gibson@socrata.com", "******", "******");
    v.create(new File("/Users/sam/Desktop/robots.csv"), conn);

Appending to an existing dataset
--------------------------------

    Connection c = new HttpConnection("robots.dod.gov", "sam.gibson@socrata.com", "******", "******");
    View v = View.find("robo-tics", conn);
    v.append(new File("/Users/sam/Desktop/super-secret-robots.csv"), conn);

Replacing the rows in an existing dataset
-----------------------------------------

    Connection c = new HttpConnection("robots.dod.gov", "sam.gibson@socrata.com", "******", "******");
    View v = View.find("robo-tics", conn);
    v.replace(new File("/Users/sam/Desktop/snidely-whiplash-robots.csv"), conn);

Publishing a dataset (Publishing sandbox-only)
----------------------------------------------

Note that currently the socrata API doesn't support publishing. There is a publishing playground if you wish to test the publishing feature before they're released and make sure that all your applications work as expected.

    Connection c = new HttpConnection("robots.dod.gov", "sam.gibson@socrata.com", "******", "******");
    View v = View.find("robo-tics", conn);
    View newlypublished = v.publish(conn);

Creating an editable copy of a dataset
--------------------------------------

Note that currently the socrata API doesn't support publishing. There is a publishing playground if you wish to test the publishing feature before they're released and make sure that all your applications work as expected.


    Connection c = new HttpConnection("robots.dod.gov", "sam.gibson@socrata.com", "******", "******");
    View v = View.find("robo-tics", conn);
    View newlyeditable = v.copy(conn);
    // [...] perform some edit operation on it.
