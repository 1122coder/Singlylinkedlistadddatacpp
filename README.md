# Singlylinkedlistadddatacpp

#include <iostream>

using namespace std;

struct Snode {
    int number;
    string name;
    string salary;
    string department;

    Snode *next;

};

class list {
private:
    Snode *head, *tail;
public:
    list();
    //void ~list();
    bool new_node(int number, string name, string salary, string department);
    bool insert_at_beginning(int number, string name, string salary, string department);
    bool insert_at_location (int number, string name, string salary, string department , int node_no);
    bool insert_at_end(int number, string name, string salary, string department);
    bool del_fir_record();
    bool del_at_end();
    bool del_at_location(int no);
    void display();

};

list::list()
{
    head =  tail= NULL;
}

//list::~list()

bool list::new_node(int number, string name, string salary ,string department)
{
     Snode *temp = new Snode;
     temp->number = number;
     temp->name = name;
     temp->salary = salary;
     temp->department = department;

     temp->next =NULL;
     if(!head){
        head=temp;
        tail=temp;
        temp= NULL;
        return true;
     }  else {
     tail->next = temp;;
     tail= tail->next;
     return true;
     }
     return false;
}

bool list::insert_at_beginning(int number, string name, string salary, string department){

    Snode *temp=new Snode;
    temp->number=number;
    temp->name=name;
    temp->salary=salary;
    temp->department=department;
    temp->next=NULL;

    if(!head){
        cout<<"Sorry! List does not exits!"<<endl;
        return false;
    }else {
        temp->next=head;
        head=temp;
        return true;
    }
    return false;
}

bool list::insert_at_location (int number, string name, string salary, string department, int node_no){
    if(!head){
        cout<<"Sorry! There is no list to be proceed"<<endl;
        return false;
    }else {
        int count_node=1;
        Snode *Trav=new Snode;
        Trav=head;

        while(Trav !=NULL ){

            if(count_node == node_no){
                Snode *temp=new Snode;
                temp->number=number;
                temp->name=name;
                temp->salary=salary;
                temp->department=department;
                temp->next=NULL;

                    if(Trav->next != tail){
                        temp->next=Trav->next;
                        Trav->next=temp;
                        return true;
                    }else if(Trav->next == tail){
                        Trav->next=temp;
                        tail=tail->next;
                        return true;
                    }
            }
            count_node++;
            Trav=Trav->next;
        }
    }
    return false;
}

bool list::insert_at_end(int number, string name, string salary, string department){
                Snode *temp=new Snode;
                temp->number=number;
                temp->name=name;
                temp->salary=salary;
                temp->department=department;
                temp->next=NULL;
                if(!head){
                    cout<<"Sorry no data allocated"<<endl;
                    return false;
                }
                else{
                        tail->next=temp;
                        tail=tail->next;
                        return true;
                }
                return false;
}

bool list::del_fir_record(){
    if(!head){
        cout<<"No record Exits"<<endl;
        return false;
    }else {
    Snode *fir = new Snode;
    fir=head;
    head=head->next;
    fir->next=NULL;
    delete fir;
    return true;
    }
    return false;
}

bool list::del_at_end(){
    if(!head){
         cout<<"No record Exits"<<endl;
        return false;
    }else {
        Snode *tem=new Snode;
        tem=head;
        while(tem->next !=tail){
            tem=tem->next;
        }
        tail=tem;
        tem=tem->next;
        tail->next=NULL;;
        tem->next=NULL;
        delete tem;

        return true;
    }
    return false;
}

bool list::del_at_location(int no){
    Snode *current=NULL;
    if(head){
        current=head;
    }
    if( no == 1){
        head=head->next;
        current->next=NULL;
        delete current;
        return false;
    }else if(no > 1){
        int count_no=1;
        Snode *prev;
        prev=NULL;
    while(current != NULL){
        if(count_no == no && current==tail ){
           prev->next=NULL;
           tail=prev;
           delete current;
           return true;
        }else if(count_no == no && current!=tail){
             prev->next=current->next;
            current->next=NULL;
            delete current;
            return true;
        }
        prev=current;
        current=current->next;
        count_no++;
        }
    }
    return false;
}

void list ::display(){
    if(!head){
        cout<<"Data not Available!"<<endl;
    }
    else{
        Snode *Trav= new Snode;
        Trav=head;
        while(Trav !=NULL){
            cout<<"Employee Data:"<<endl;
            cout<<"Roll.Number:"<<Trav->number<<endl;
            cout<<"Name:"<<Trav->name<<endl;
            cout<<"Salary:"<<Trav->salary<<endl;
            cout<<"Department:"<<Trav->department<<endl;

            Trav = Trav->next;
        }
    }
}

int main()
{
    list obj;
    obj.new_node(515786, "Malik Muhammad Kashif Saeed", "350 K" , "Software Hub");
    obj.display();

    cout<<"---------------------------"<<endl;
    obj.insert_at_beginning(515846, "Muhammad Siddiqi", "400 K" , "Software Hub");
    obj.display();

    cout<<"---------------------------------"<<endl;
    obj.insert_at_end(515846, "Muhammad Zeeshan", "375 K" , "Software Hub");
    obj.display();

    cout<<"---------------------------------"<<endl;
    obj.del_fir_record();
    obj.display();
    cout<<"---------------------------------"<<endl;
    obj.del_at_end();
    obj.display();

     cout<<"---------------------------------"<<endl;
     obj.del_at_location(1);
     obj.display();

    return 0;
}
