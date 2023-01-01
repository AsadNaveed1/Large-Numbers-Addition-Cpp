// Wrriten by: Muhammad Asad Naveed
// U.No: 3035957848
// Assignment 3 Question 1
// Description:  In this question, you are going to implement addition of two arbitrarily large numbers using linked lists.

#include <iostream>
#include <iomanip>
#include <string>
#include <cctype>
#include <cstdlib>

using namespace std;



struct Node
{
    int value;
    Node * next;
};

void delete_list(Node * & n3);

// output the linked list
void print_list(Node * head)
{
    Node * current = head;
    while (current != NULL)
    {
        // process the current node, e.g., print the content
        cout << current->value << " -> ";
        current = current->next;
    }
    cout << "NULL\n";
}


//function to print sum in its conventional form.
void output_final (Node * &n3)
{
    
    string output_value;
    Node *t = n3;

    while(t->next != NULL)
    {
        output_value = to_string(t->value) + output_value;         //converted to string for outputing
        if (t->value < 10)                    //if the value in the new list is less then 10 two zeroes are output (00)
        {
            output_value = "00" + output_value;

        }
            
        else if (t->value < 100)             //if the value is less then 100 only one zero is output (0)
        {
            output_value = "0" + output_value;

        }
            
        t = t->next;                         //moved to next value
    }
    output_value = to_string(t->value) + output_value;

    cout << output_value << endl;

    delete_list(n3);

}

// output the large number stored in the linked list
void print_num(Node * head)
{
    Node * current = head;
    while (current != NULL)
    {
        if (current == head)
            cout << current->value;
        else
            cout << setw(5) << setfill('0') << current->value;
        current = current->next;
    }
}

// insert a value as a node to the head of a linked list
void head_insert(Node * & head, int v)
{
    Node * p = new Node;
    p->value = v;
    p->next = head;
    head = p;
}

//this creates list in forward manner
void forward_insert(Node *&head, Node *&tail, int v)
{
    Node *p = new Node;
    p->value = v;
    p->next = NULL;

    if (head == NULL)            //if first node both head and tail pointing to it
    {
        head = p;
        tail = p;
    }
    else
    {
        tail->next = p;          //tail points to the last node of the link list
        tail = p;
    }
}


// delete the head node from a linked list
void delete_head( Node * & head)
{
    if (head != NULL) {
        Node * p = head;
        head = head->next;
        delete p;
    }
}

// free an entire linked list
void delete_list(Node * & head)
{
    while ( head != NULL )
    {
        delete_head(head);
    }
}

// double the capacity of an array
// array: input array
// size: original size of array, updated to new size of array
void grow_array( char * & array, int & size )
{
    if (array == NULL)
        return;

    int newSize = size * 2;

    // doubled the size of the array;
    char * tmp = new char [ newSize ];
    // copy original contents
    for (int i = 0; i < size; ++i)
        tmp[i] = array[i];

    delete [] array;

    array = tmp;
    size = newSize;
}

// get a number from a user
// by reading character by character until a space is hit
// use dynamic array to store the digits
// digits:  character array that stores the digits of the number
// numDigits: number of digits read from input
void input_num(char * & digits, int & numDigits)
{
    int arraysize = 32;
    digits = new char [arraysize];
    char c;
    int numRead = 0;

    // read each digit as a character until a white space is hit
    c = cin.get();
    while (!isspace(c))
    {
        if (numRead >= arraysize)
            grow_array( digits, arraysize );

        digits[numRead] = c;
        numRead++;

        c = cin.get();
    }

    numDigits = numRead;

}

// get a large integer from user input
// and store in a linked list of Node
// each node stores the value of a chunk of 5 digits taken from the large integer
// e.g., if the input is 43323000089500012, the linked list is
// 43 -> 32300 -> 895 -> 12 -> NULL
//
Node * create_num_list()
{
    // TASK 1a: declare a pointer pointing to the head of the link list
    Node * head = NULL;
    Node * tail = head;


    string str;
    char * digits = NULL;  // a dynamic array for storing an input number
    int numDigits;
    int val;

    // get a number from the user
    input_num( digits, numDigits);

    // scan the digits in reverse, and create a list of nodes for
    // the value of every 5 digits
    str.clear();
    for (int i = numDigits-1; i >=0; --i) {
        str = digits[i] + str;
        if (str.length()==3) {
            val = atoi(str.c_str());

            // TASK 1b: insert a value as a node to the head of the linked list
            forward_insert(head, tail, val);

            str.clear();
        }
    }
    // the digits array is scanned and there are still digits
    // stored in str that are not inserted into the list yet
    if (!str.empty()) {
        val = atoi(str.c_str());

        // TASK 1c: insert a value as a node to the head of the linked list
        forward_insert(head, tail, val);
    }

    if (digits != NULL) {
        delete [] digits;

    }

    // TASK 1d: return the pointer to the linked list
    return head;
}



// return the length of a linked list
int list_length(Node * head)
{
 	// TASK 3: Modify this print function to one that
	// count the number of nodes in a linked list

    int num = 0;

    Node * current = head;
    while (current != NULL)
    {
        // process the current node, e.g., print the content
        ++num;
        current = current->next;
    }

    return num;
}

// return if the number n1 is larger than n2
bool larger(Node * n1, Node * n2)
{
    int len1 = list_length(n1);
    int len2 = list_length(n2);
    Node *head = NULL;

	// TASK 4a: handle the case
	// when the list lengths are different
    if (len1 > len2)
        return true;
    else if (len1 < len2)
        return false;

    // the two lists are of equal length

    Node * curr1 = n1, * curr2 = n2;

    while (curr1 != NULL) {
        if (curr1->value > curr2->value)
            return true;
        else if (curr1->value < curr2->value)
            return false;

        // TASK 4b: advance curr1, curr2
		// to point to the next nodes
        curr1 = curr1->next;
        curr2 = curr2->next;
    }

    return false;
}

//this is the addition function that adds both the list to result in the new list
void add_list (Node *n1, Node *n2)
{
    int len1 = list_length(n1);
    int len2 = list_length(n2);
    Node *head = NULL;


    Node *larger= NULL;
    Node *small = NULL;

    if (len1 > len2)           //finding which list is larger of the two
    {
        larger = n1;
        small = n2;
    }
    else
    {
        larger = n2;
        small= n1;
    }

    Node *n3 = NULL;                //n3 is pointing to null initially
    Node *tail= NULL;               //tail is also pointing to null intially

    int sum = 0;
    int carry = 0;

    while (larger != NULL )        //going til the end of the larger list
    {
        if (small != NULL)          //if end of small list is not reached
        {
            sum = larger->value + small->value;

            if (carry == 1)         //checks if there is a carrying number
            {
                sum = sum +1;
                carry= 0;             //makes the carry value zero again
            }




            if (sum >= 1000)    //checks if sum is greater then equal to 1000
            {
                
                sum = sum % 1000;    // e.g if sum is 1098 we get 98
                carry = 1;           //1 is carried to next node

            }

            forward_insert(n3, tail, sum);       //inserts the sum

 
            small = small->next;            //both small and large list moving to the next node
            larger = larger->next;

        }

        else                             //if end of small list reached but end of large has not
        {
            sum = larger->value;         

            if (carry == 1)              // checks if there is a carry number
            {
                sum = sum+1;
                carry = 0;
            }



            if (sum >= 1000)             //checks if sum greater then equal to 1000 
            {
                sum = sum % 1000;
                carry = 1;
                

            }

            forward_insert(n3, tail, sum);

            larger = larger->next;        //moving to the next value of the larger list


        }

        

    }

    if (carry == 1)                      //checks if there is some value left to be carried
    {
        forward_insert(n3, tail, carry);
    }    
    print_list(n3);                    //prints the linked linked list storing the sum of the two numbers.


    output_final(n3);                   // calls the output function to print out the final sum in its conventional form.
  

}

//this is the main function
int main()
{
    Node * n1, * n2;


    n1 = create_num_list();               //creates linked list from the input
    cin.get();       // skip the '>' sign
    cin.get();       // the space after the '>' sign
    n2 = create_num_list();              //creates linked list from the

    // TASK 2: call print_list() on n1 and n2 for checking
    print_list(n1);
    print_list(n2);

    add_list(n1, n2);        //call the addition function to add both the list and output the resulting list

    // TASK 5: free the linked lists
    delete_list(n1);           
    delete_list(n2);

    return 0;
}
