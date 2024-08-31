public class Interview {

    public static void display(Node head) {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
        System.out.println(); // Move to the next line after display
    }

    public static Node nthValueFromEnd(Node head, int n) {
        if (head == null || n < 0) {
            return null; // Invalid input
        }

        Node fast = head;
        Node slow = head;

        // Move fast pointer n steps ahead
        for (int i = 0; i < n; i++) {
            if (fast == null) {
                return null; // n is greater than the length of the list
            }
            fast = fast.next;
        }

        // Move both fast and slow 
        while (fast != null) {
            fast = fast.next;
            slow = slow.next;
        }

        return slow; // slow is now at the nth node from the end
    }
    public static Node nthValueDelete(Node head, int n) {
        if (head == null || n < 0) {
            return head; // Invalid input or empty list
        }

        Node fast = head;
        Node slow = head;

        // Move fast pointer n steps ahead
        for (int i = 0; i < n; i++) {
            if (fast == null) {
                return head; // n is larger than the length of the list
            }
            fast = fast.next;
        }

        if (fast == null) {
            return head.next; // New head of the list
        }

        // Move both fast and slow 
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }

        // Skip the node to be deleted
        if (slow.next != null) {
            slow.next = slow.next.next;
        }

        return head; // Return the updated head of the list
    }

    public static class Node {
        int data;
        Node next;

        Node(int data) {
            this.data = data;
            this.next = null; // Ensure next is initialized
        }
    }

    public static void main(String[] args) {
        Node a = new Node(5);
        Node b = new Node(10);
        Node c = new Node(51);
        Node d = new Node(1);
        Node e = new Node(8);

        a.next = b;
        b.next = c;
        c.next = d;
        d.next = e;

        display(a);

        //  deletion
        a = nthValueDelete(a, 0); // Delete head
        display(a);

        // nthValueFromEnd
        Node r = nthValueFromEnd(a, 2); // Changed from 3 to 2 for the new list
        if (r != null) {
            System.out.println(r.data);
        } else {
            System.out.println("Node not found");
        }
    }
}
