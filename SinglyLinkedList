import java.util.Scanner;

public class SinglyLinkedList {
	
	static Scanner sc = new Scanner(System.in);
	
	static boolean incognito = false;
	static boolean end = false;
	
	// IMPORTANT
	static class node {
		String data;
		node next;
		node (String value) {
			data = value;
			next = null;
		}
	}
	static node head;

	// stacks at the beginning
	static void addWebsite(String data) {
		//create a link
		node lk = new node(data);;
		// point it to old first node
		lk.next = head;
		//point first to new first node
		head = lk;
	}

	// for incognito, deletes head node
	static void incognitoMode() {
		head = head.next;
	}
	
	static boolean deleteWebsite(String key) {
		node temp = head;
		node prev = null;
		
		String t = temp.data;
		if (temp != null && t.contains(key)) {
			head = temp.next; return true;
		}
		// Find the key to be deleted
		while (temp != null && !(t.contains(key))) {
			prev = temp;
			temp = temp.next;
			t = temp.data;
		}
		// If the key is not present
		if (temp == null) return false;
		// Remove the node
		prev.next = temp.next;
		return true;
	}
	
	// delete full history
	static void deleteHistory(node linkedlist){
		if(linkedlist.next != null) {
			while(linkedlist.next.next != null) {
				linkedlist = linkedlist.next;
			}
			linkedlist.next = null;
			deleteHistory(linkedlist); // recursive
		}
		else {
			head = null;
		}
	}
	
	// checks if website is in history
	static boolean searchHistory(String key) {
		node temp = head;
		while(temp != null) {
			String t = temp.data;
			if (t.contains(key)) {
				deleteWebsite(key);
				addWebsite(key);
				return true;
			}
			temp=temp.next;
		}
		return false;
	}
	
	
	public static void main(String[] args) {
		
		if(!end) {
			int command = theBrowser();
			optionsManager(command);
		}
		else {
			System.out.println("\nTHANK YOU FOR BROWSING");
			System.exit(0);
		}
		
	}
	
	static int theBrowser() {
		
		System.out.println("***************   BROWSER   ***************\n");
		System.out.println("[1] Open Website\n"
						+  "[2] Open History\n"
						+  "[3] Incognito Mode\n"
						+  "[0] Close Browser\n");
		System.out.print("Enter option: ");
		
		int command = -1;
		try {
			command = Integer.parseInt(sc.nextLine());
			return command;
		} catch(NumberFormatException e) {
			System.out.println("\nEnter a VALID option.");
			main(null);
		}
		
		return command;
		
	}
	
	static void optionsManager(int command) {
		
		switch(command) {
		case 1:
			openWebsite();
			break;
		case 2:
			openHistory();
			break;
		case 3:
			incognito = true;
			openWebsite();
			break;
		case 0:
			System.exit(0);
			break;
		}
		
	}
	
	static void optionsManager2(String web) {
		
		switch(web) {
		case "CTRL+I":
			if(incognito) incognito = false;
			else {
				incognito = true;
				addWebsite("INCOGNITO MODE");
			}
			openWebsite();
			break;
		case "CTRL+H":
			openHistory();
			break;
		case "CTRL+E":
			end = true;
			main(null);
			break;
		}
		
	}
	
	static void optionsManager3() {
		
		System.out.println("HISTORY OPTIONS: "
				+ "\n[1] Search History"
				+ "\n[2] Delete Website Visit"
				+ "\n[3] Clear History"
				+ "\n[0] Browse More");
		System.out.print("Enter option: ");
		
		int command = -1;
		try {
			command = Integer.parseInt(sc.nextLine());
			switch(command) {
			case 1:
				System.out.print("\nSearch website: ");
				String searchKey = sc.nextLine();
				if(!(searchKey.contains(".com")))	searchKey = searchKey + ".com";
				if(searchHistory(searchKey)) {
					System.out.println("\nWebsite is found. Opening website...");
					openWebsite();
				}
				else {
					System.out.println("\nWebsite is NOT found.");
					openHistory();
				}
				break;
			case 2:
				System.out.print("\nDelete website: ");
				String delKey = sc.nextLine();
				if(deleteWebsite(delKey)) {
					System.out.println("\nDelete was successful.");
				}
				else {
					System.out.println("\nWebsite is NOT found.");
				}
				openHistory();
				break;
			case 3:
				node p = head;
				deleteHistory(p);
				openHistory();
				break;
			case 0:
				openWebsite();
				break;
			}
		} catch(NumberFormatException e) {
			System.out.println("\nEnter a VALID option.");
			optionsManager3();
		}
		
	}
	
	static void openWebsite() {
		
		node p = head;
		if(incognito)	System.out.println("\nIncognio Mode is ON");
		if(p != null) {
			System.out.println("\n\nYou are currently browsing " + p.data + ".\n");
			System.out.println("CONTROL OPTIONS: "
					+ "\nCTRL+I = Turn ON/OFF Incognito"
					+ "\nCTRL+H = Open History"
					+ "\nCTRL+E = Exit Browser");
			if(incognito)	incognitoMode();
		}
		System.out.print("\nEnter a website: ");
		String web = sc.nextLine();
		if(web.contains("CTRL+I") || web.contains("CTRL+H") || web.contains("CTRL+E"))
			optionsManager2(web);
		else {
			if(!(web.contains(".com")))	web = web + ".com";
			addWebsite(web);
		}
		openWebsite();
		
	}
	
	// uses traversal operation
	static void openHistory() {
		
		node p = head;
		System.out.println("\nBROWSER HISTORY:");
		if(p == null) {
			System.out.println("\nBrowsing History is Empty.\nOpening Browser...");
			openWebsite();
		}
		System.out.println();
		//start from the beginning
		while(p != null) {
			System.out.println(p.data);
			p = p.next;
		}
		System.out.println("\n");
		optionsManager3();
		
	}

}
