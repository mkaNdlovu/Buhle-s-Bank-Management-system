# Buhle-s-Bank-Management-system
This is a cpp project that i am currently working on. It is a bank Management system, that provides a comprehensive and efficient solution for managing customer accounts,transactions and other core banking functiions, with its robust security measures and user friendly features as well asideal solutions for Financial institutions to streamline their operations and improve their customer satisfaction. feel free to add on to this code.
Key features:
Customer account Management

/*
Buhle's Bank Management system
created by Buhle Mdlongwa Ndlovu
Date : 05 April 2025
N.B This is still some work in progress.
*/

#include <iostream>
#include<fstream>
#include<cctype>
#include<iomanip>

using namespace std;

class account
{
    int acno;
    char name[50];
    int deposit;
    char type;
public:
    void create_account();
    void show_account()const;
    void modify();
    void dep(int);
    void draw(int);
    void report() const;
    int retacno ()const;
    int retdeposit()const;
};

void  account::create_account()
{
    system("clear");
    cout<<"\n\t\t\tEnter the account no: ";
    cin>>acno;
    cout<<"\n\t\t\tEnter the name of the account holder here: ";
    //cin>>ignore();
    string name[50];
    //cin>>getline(name, 50);
    cout<<"\n\t\t\tEnter Type of the account (C/S): ";
    cin>>type;
    cin>>type;
    cout<<"\n\t\t\tEnter the initial amount: R ";
    cin>>deposit;
    cout<<"\n\t\t\tEnter the account no: ";
    cin>>acno;
    cout<<"\n\t\t\tAccount has been created... ";
    cout<<"======================================";

}void  account::show_account()const
{

    cout<<"\n\t\t\tAccount No: "<<acno;
    cout<<"\n\t\t\tAccount holder name: ";
    cout<<name;
    cout<<"\n\t\t\tType of account: "<<type;
    cout<<"\n\t\t\tBalance amount: " << deposit;

}
void  account::modify()
{
    system("clear");
    cout<<"\n\t\t\tAccount no: "<<acno;
    cin>>acno;
    cout<<"\n\t\t\tModify Account Holder name: ";
    //cin>>ignore();
    //cin>>getline(name,50);
    cout<<"\n\t\t\tModify Type of the account : ";
    cin>>type;
    //cin>>toupper(type);
    cout<<"\n\t\t\tModify Balance amount: ";
    cin>>deposit;

}
 void account::dep(int x)
 {
     deposit += x;
 }
void account::draw(int x)
{

     deposit -= x;
}
void account::report()const
{
    cout<<acno<< setw(10) << " " << name << setw(10)<< type << setw(6) << deposit<< endl;
}
int account::retacno()const
{
    return acno;
}
int account::retdeposit()const
{
    return deposit;
}
//char account::rettype()const
//{
   // return type;
//}


void write_account();
void display_sp(int);
void modify_account(int);
void delete_account(int);
void display_all();
void deposit_withdraw(int, int);

int main()
{
    char ch;
    int num;
    do
    {
        system("CLS");
        cout<<"\n\t\t\t============================\n ";
        cout<<"\n\t\t\tBUHLE BANK MANAGEMENT SYSTEM ";
        cout<<"\n\t\t\t=============================\n";


        cout<<"\n\t\t\tMAIN MENU:: \n ";
        cout<<"\n\t\t\t\t1. NEW ACCOUNT ";
        cout<<"\n\t\t\t\t2. DEPOSIT AMOUNT ";
        cout<<"\n\t\t\t\t3. WITHDRAW AMOUNT";
        cout<<"\n\t\t\t\t4. BALANCE ENQUIRY ";
        cout<<"\n\t\t\t\t5. ALL ACCOUNT HOLDER LIST";
        cout<<"\n\t\t\t\t6. CLOSE AN ACCOUNT";
        cout<<"\n\t\t\t\t7.MODIFY AN ACCOUNT";
        cout<<"\n\t\t\t\t8.EXIT";
        cout<<"\n\n\t\t\t\tSelect Your Option (1-8): ";
        cin>>ch;

        switch(ch)
        {

        case '1':
            write_account();
            break;
        case '2':
            system("CLS");
            cout<<"\n\n\t\t\tEnter The account No. :";
            cin>> num;
            deposit_withdraw(num, 1);
            break;
        case '3':
            system("CLS");
            cout<<"\n\n\t\t\tEnter The account No. :";
            cin>> num;
            deposit_withdraw(num, 2);
            break;
        case '4':
            system("CLS");
            cout<<"\n\n\t\t\tEnter The account No. :";
            cin>> num;
            display_sp(num);
            break;
        case '5':
            display_all();
            break;
        case '6':
            system("CLS");
            cout<<"\n\n\t\t\tEnter The account No. :";
            cin>> num;
            delete_account(num);
            break;
        case '7':
            system("CLS");
            cout<<"\n\n\t\t\tEnter The account No. :";
            cin>> num;
            modify_account(num);
            break;
        case '8':
            system("CLS");
            cout<<"\n\n\t\t\tBrought to you by Buhle Mdlongwa Ndlovu";
            break;
        default: cout<<"\a";
        }
        cin.ignore();
        cin.get();
    }while(ch != '8');
    return 0;

}
void write_account()
{
    account ac;
    ofstream outFile;
    outFile.open("account.dat", ios::binary| ios::app);
    ac.create_account();
    outFile.write(reinterpret_cast<char*> (&ac), sizeof(account));
    outFile.close();
}
void display_sp(int n)
{
    account ac;
    bool flag = false;
    ifstream inFile;
    inFile.open("account.dat", ios::binary);
    if(!inFile)
    {
      cout<<"File could not be open!!! Please press any key...";
      return;
    }
    cout<< "\n\t\t\tBALANCE DETAILS\n";
    while(inFile.read(reinterpret_cast<char*>(&ac), sizeof(account)))
    {
        if(ac.retacno()== n)
        {
            ac.show_account();
            flag = true;
        }
    }
    inFile.close();
    if(flag == false)
        cout<<"\n\n\t\t\tAccount number does not exist";
}
    //File.close();
    //if(found == false)
//cout << "\n\n\t\t\tRecord Not Found";

//}
void modify_account(int n)
{
    bool found = false;
    account ac;
    fstream File;
    File.open("account.dat", ios::binary |ios::in |ios::out);
    if(!File)
    {
        cout<<"File could not be opened! Please press any key....";
        return;
    }
    while(!File.eof() && found == false)
    {
        File.read(reinterpret_cast<char*> (&ac), sizeof(account));
        if(ac.retacno() == n)
        {
            ac.show_account();
            cout<<"\n\n\t\t\tEnter the new Detailsof the account: "<<endl;
            ac.modify();
            int pos = (-1) * static_cast<int> (sizeof(account));
            cout << "\n\n\t\t\tRecords updated";
            found = true;
        }
    }
    File.close();
    if (found == false)
        cout<< "\n\n\t\t\Records not found";
}
void delete_account(int n)
{
    account ac;
    ifstream inFile;
    ofstream outFile;
    inFile.open("account.dat", ios::binary);
    if(!inFile)
    {
      cout<<"File could not be open!!! Please press any key...";
      return;
    }
    outFile.open("Temp.dat", ios::binary);
    inFile.seekg(0, ios::beg);
    while(inFile.read(reinterpret_cast<char*>(&ac), sizeof(account)))
    {
        if(ac.retacno() != n)
        {
            outFile.write(reinterpret_cast<char*> (&ac), sizeof(account));
        }
    }
    inFile.close();
    outFile.close();
    remove("account.dat");
    rename("Temp.dat", "account.dat");
    cout<<"\n\nRecord Deleted..";
}
void display_all()
{
    system("CLS");
    account ac;
    ifstream inFile;
    inFile.open("account.dat", ios::binary);
    if(!inFile)
    {
      cout<<"File could not be open!!! Please press any key...";
      return;
    }
    cout<< "\n\t\t\tBALANCE DETAILS\n";
    cout<<"======================================\n";
    cout<<"A/c no.     NAME    Type    Balance\n";
    cout<<"======================================\n";
    while(inFile.read(reinterpret_cast<char*>(&ac), sizeof(account)))
    {
        ac.report();
    }
    inFile.close();
}

void deposit_withdraw(int n, int option)
{
    int amt;
    bool found = false;
    account ac;
    fstream File;
    File.open("account.dat", ios::binary| ios::in | ios::out);
    if(!File)
    {
      cout<<"File could not be open!!! Please press any key...";
      return;
    }
    while(!File.eof() && found ==false)
    {
        File.read(reinterpret_cast<char*>(&ac), sizeof(account));

        if(ac.retacno()== n)
        {
            ac.show_account();
            if (option == 1)
            {
                cout<<"\n\n\t\t\tTOdEPOSITS AMOUNT";
                cout<<"\n\n\t\t\tEnter the amount to be deposited: ";
                cin>>amt;
                ac.dep(amt);
            }
            if(option == 2)
            {
                 cout<<"\n\n\t\t\tTO WITHDRAW AMOUNT";
                cout<<"\n\n\t\t\tEnter the amount to be withdrawn: ";
                cin>>amt;
                int bal = ac.retdeposit() - amt;
                if(bal < 0)
                    cout<<"Insufficient balance, please deposit cash into your account";
                else
                ac.draw(amt);
            }
            int pos = (-1) * static_cast<int>(sizeof(ac));
            File.seekp(pos, ios::cur);
            File.write(reinterpret_cast<char*>(&ac), sizeof(account));
            cout<< "\n\n\t\t\tRecords updated";
            found == true;
        }
    }
    File.close();
    if(found == false)
       cout << "\n\n\t\t\tRecord Not Found";
}
