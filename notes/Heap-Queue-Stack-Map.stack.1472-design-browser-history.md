---
id: 97widkzw6vnh13n97dcyo89
title: 1472-design-browser-history
desc: ''
updated: 1689256442838
created: 1689252925744
---
## #medium #stack #ood

You have a browser of one tab where you start on the homepage and you can visit another url, get back in the history number of steps or move forward in the history number of steps.

Implement the BrowserHistory class:

BrowserHistory(string homepage) Initializes the object with the homepage of the browser.
void visit(string url) Visits url from the current page. It clears up all the forward history.
string back(int steps) Move steps back in history. If you can only return x steps in the history and steps > x, you will return only x steps. Return the current url after moving back in history at most steps.
string forward(int steps) Move steps forward in history. If you can only forward x steps in the history and steps > x, you will forward only x steps. Return the current url after forwarding in history at most steps.

## 解题思路

dual stack贼慢，想办法做成double linked list或者two pointer array

### 普通解法

class BrowserHistory {
    Stack<String> back;
    Stack<String> forward;
    public BrowserHistory(String homepage) {
        back = new Stack<>();
        forward = new Stack<>();
        back.push(homepage);
    }
    
    public void visit(String url) {
        back.push(url);
        while (!forward.isEmpty()) forward.pop();
    }
    
    public String back(int steps) {
        while (back.size() > 1 && steps-- != 0) {
            forward.push(back.pop());
        }
        return back.peek();
    }
    
    public String forward(int steps) {
        while (!forward.isEmpty() && steps-- != 0) {
            back.push(forward.pop());
        }
        return back.peek();
    }
}

### array two pointer解法

class BrowserHistory {
    private List<String> URLsHistory;
    private int currURL;
    private int lastURL;
    
    public BrowserHistory(String homepage) {
        URLsHistory = new ArrayList<>();
        URLsHistory.add(homepage);
        currURL = 0;
        lastURL = 0;
    }
    
    public void visit(String url) {
        currURL++;
        if (URLsHistory.size() > currURL) {
            URLsHistory.set(currURL, url);
        }
        else {
            URLsHistory.add(url);
        }
        lastURL = currURL;
    }
    
    public String back(int steps) {
        currURL = Math.max(0, currURL - steps);
        return URLsHistory.get(currURL);
    }
    
    public String forward(int steps) {
        currURL = Math.min(lastURL, currURL + steps);
        return URLsHistory.get(currURL);
    }
}

### double linked list

// A class to represent a node in a linked list
class Node {
  // The previous and next nodes in the list
  public Node prev;
  public Node next;
  // The URL represented by this node
  public final String url;
  
  // Constructor that sets the URL for this node
  public Node(final String url) {
    this.url = url;
  }
}

// A class to represent a browser history
class BrowserHistory {
  // The current node in the history
  private Node curr;
  
  // Constructor that creates a new history with the given homepage
  public BrowserHistory(String homepage) {
    // Create a new node to represent the homepage
    curr = new Node(homepage);
  }

  // Method to add a new URL to the history
  public void visit(String url) {
    // Create a new node to represent the new URL
    curr.next = new Node(url);
    // Set the previous node for the new node to be the current node
    curr.next.prev = curr;
    // Make the new node the current node
    curr = curr.next;
  }

  // Method to navigate back in the history by the given number of steps
  public String back(int steps) {
    // While there are previous nodes and we haven't gone back enough steps yet
    while (curr.prev != null && steps-- > 0) {
      // Move back one node by setting the current node to the previous node
      curr = curr.prev;
    }
    // Return the URL represented by the current node
    return curr.url;
  }

  // Method to navigate forward in the history by the given number of steps
  public String forward(int steps) {
    // While there are next nodes and we haven't gone forward enough steps yet
    while (curr.next != null && steps-- > 0) {
      // Move forward one node by setting the current node to the next node
      curr = curr.next;
    }
    // Return the URL represented by the current node
    return curr.url;
  }
}


