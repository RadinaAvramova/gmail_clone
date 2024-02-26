# Gmail Clone in Dart
Welcome to the Gmail Clone in Dart project! This project is an attempt to replicate the core features and functionalities of the popular email service Gmail using Dart programming language and Flutter framework. With Gmail Clone in Dart, users can experience a familiar email interface, compose and send emails, manage their inbox, and much more.

## Features
1. **Email Inbox:** Displays a list of received emails in the user's inbox, showing important details such as sender, subject, and timestamp.

2. **Compose Email:** Allows users to compose new emails, providing fields for entering recipient(s), subject, message body, and optional attachments.

3. **Email Viewing:** Enables users to view the content of individual emails, including HTML and plain text formatting, inline images, and attachments.

4. **Email Search:** Provides a search functionality to help users quickly find specific emails based on criteria such as sender, subject, date, or keywords.

5. **Email Sorting and Filtering:** Supports sorting and filtering options to organize emails based on various attributes such as date, sender, importance, or labels.

6. **Email Labels and Categories:** Allows users to categorize and label emails for better organization and easier navigation within the inbox.

7. **Email Drafts and Auto-Save:** Auto-saves email drafts periodically to prevent data loss and allows users to resume composing emails where they left off.

8. **Email Notifications:** Sends notifications to users for new incoming emails, ensuring they stay updated on their email activity.

## Installation
To run the Gmail Clone in Dart project locally, follow these steps:

1. **Clone the Repository:** Clone the repository to your local machine using the following command:

git clone https://github.com/RadinaAvramova/gmail_clone.git

2. **Navigate to the Directory:** Change your current directory to the location of the cloned repository:

cd gmail_clone

3. **Install Dependencies:** Install the required dependencies by running:

flutter pub get

4. **Run the Application:** Start the application by running:

flutter run

5. **Access the App:** Once the application is running, access the Gmail Clone in Dart through an emulator or physical device to start exploring its features.

## Usage
1. **Login or Sign Up:** Start by logging in to your email account or sign up for a new account if you don't have one.

2. **Navigate Inbox:** Explore your email inbox to view received emails, and click on individual emails to read their content.

3. **Compose Email:** Click on the compose button to start composing a new email, then fill in the necessary fields and click send to dispatch the email.

4. **Search and Filter Emails:** Use the search bar to find specific emails by sender, subject, or keywords, and apply filters to narrow down search results.

5. **Manage Emails:** Manage your emails by marking them as read/unread, archiving, deleting, or labeling them to keep your inbox organized.

## Customization
You can customize the Gmail Clone in Dart project by modifying aspects such as the user interface design, email management features, authentication methods, integration with email APIs, and additional functionalities such as email threading, conversation view, or advanced search options.


## Screenshots

![listview](https://github.com/AppleEducate/gmail_clone/blob/master/screenshots/listview.png)

![details](https://github.com/AppleEducate/gmail_clone/blob/master/screenshots/details.png)

![tablet](https://github.com/AppleEducate/gmail_clone/blob/master/screenshots/tablet.png)

![selection](https://github.com/AppleEducate/gmail_clone/blob/master/screenshots/selection.png)


## Example 

``` dart
import 'package:floating_search_bar/floating_search_bar.dart';
import 'package:flutter/material.dart';
import 'package:gmail_clone/ui/app/app.dart';
import 'package:responsive_scaffold/responsive_scaffold.dart';
import 'package:responsive_scaffold/utils/breakpoint.dart';

import '../data/classes/email.dart';
import '../data/dummy_data.dart';
import 'common/common.dart';

class HomeScreen extends StatefulWidget {
  @override
  _HomeScreenState createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  List<EmailItem> _emails;
  @override
  void initState() {
    _emails = emails;
    super.initState();
  }

  final Size _tabletBreakpoint = Size(510.0, 510.0);

  @override
  Widget build(BuildContext context) {
    final bool _tablet = isTablet(context, breakpoint: _tabletBreakpoint);
    return ResponsiveScaffold.builder(
      tabletBreakpoint: _tabletBreakpoint,
      detailBuilder: (BuildContext context, int index) {
        final i = _emails[index];
        return DetailsScreen(
          appBar: AppBar(
            elevation: 0.0,
            actions: [
              IconButton(
                icon: Icon(Icons.archive),
                onPressed: () {},
              ),
              IconButton(
                icon: Icon(Icons.delete_outline),
                onPressed: () {
                  setState(() {
                    _emails.removeAt(index);
                  });
                },
              ),
              IconButton(
                icon: Icon(Icons.mail_outline),
                onPressed: () {},
              ),
              IconButton(
                icon: Icon(Icons.more_horiz),
                onPressed: () {},
              ),
            ],
          ),
          body: EmailView(
            item: i,
            favoriteChanged: () {
              setState(() {
                i.favorite = !i.favorite;
              });
            },
          ),
        );
      },
      drawer: AppDrawer(),
      tabletSideMenu: _tablet
          ? Flexible(
              flex: 1,
              child: AppSideMenu(),
            )
          : null,
      tabletFlexListView: 4,
      slivers: <Widget>[
        SliverFloatingBar(
          floating: true,
          automaticallyImplyLeading: !_tablet,
          title: TextField(
            decoration: InputDecoration.collapsed(hintText: "Search mail"),
          ),
          trailing: CircleAvatar(
            child: Text("RD"),
          ),
        ),
        SliverToBoxAdapter(
          child: Container(
            padding: EdgeInsets.all(12.0),
            child: Text("All Inboxes"),
          ),
        ),
      ],
      itemCount: _emails?.length ?? 0,
      itemBuilder: (BuildContext context, int index) {
        final i = _emails[index];
        final bool _lastItem = (index + 1) == emails?.length ?? 0;
        if (_lastItem) {
          return Container(
            padding: EdgeInsets.only(bottom: 70.0),
            child: EmailListTile(
              item: i,
              favoriteChanged: () {
                setState(() {
                  i.favorite = !i.favorite;
                });
              },
            ),
          );
        }
        return EmailListTile(
          item: i,
          favoriteChanged: () {
            setState(() {
              i.favorite = !i.favorite;
            });
          },
        );
      },
      floatingActionButton: EmailFAB(),
    );
  }
}

```
