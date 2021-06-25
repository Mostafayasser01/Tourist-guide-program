#include <iostream>
#include<string.h>
#include<string>
#include<fstream>
#include<iomanip>
using namespace std;
void form_txt() {
    fstream file;
    file.open("shop.txt", ios::in | ios::out | ios::app);
    if (!file) {
        file << "Code" << "\t";
        file << "product" << "\t\t";
        file << "Price" << "\t";
        file << "Quantity" << "\t";
        file << "sales" << "\n";
    }

    file.close();
}

void add() {
    double code, sales, price, quantity;
    string name_product;
    fstream file;
    file.open("shop.txt", ios::in | ios::out | ios::app);
    cout << "\t\t\t\t\t\tEnter Code of product : ";
    cin >> code;
    cout << "\n\t\t\t\t\t\tEnter name of product : ";
    cin >> name_product;
    cout << "\n\t\t\t\t\t\tEnter Price of product : ";
    cin >> price;
    cout << "\n\t\t\t\t\t\tEnter Quantity of product : ";
    cin >> quantity;
    cout << "\n\t\t\t\t\t\tEnter sales of product : ";
    cin >> sales;
    file << code << "\t";
    file << name_product << "\t\t";
    file << price << "\t";
    file << quantity << "\t\t";
    file << sales << "\n";
    file.close();

}
void view() {
    string detail;
    fstream file;
    file.open("shop.txt", ios::in | ios::out | ios::app);
    if (file.is_open())
    {
        while (getline(file, detail))
        {
            cout << detail << '\n';
        }
        file.close();
    }
    file.close();
}

void del() {
    int x = 0;
    string code;
    string name_product;
    string price;
    string quantity;
    string sales;
    string par;
    cout << "\t\t\t\t\t\tWarning !!!!!!!!!!!\n\t\t\t\t\t\tIf there more code for product will delete all !!!!!\n";
    cout << "\t\t\t\t\t\tEnter Code Of Product To Delete : ";
    cin >> par;
    ifstream infile;
    infile.open("shop.txt", ios::in);
    ofstream outfile;
    outfile.open("shop1.txt", ios::out);
    while (!infile.eof())
    {
        infile >> code;
        infile >> name_product;
        infile >> price;
        infile >> quantity;
        infile >> sales;
        if (!infile)break;
        if (code == par) {
            x = 1;
            continue;
        }
        else
            outfile << code << "\t" << name_product << "\t\t" << price << "\t" << quantity << "\t\t" << sales << "\n";

    }
    if(x==1)
    cout << "\t\t\t\t\t\tThis Product Is Deleted Successfully :)\n";
    else cout << "\t\t\t\t\t\tCode Is Not Found :<\n";
    infile.close();
    outfile.close();

    remove("shop.txt");
    rename("shop1.txt", "shop.txt");
}
void del_all() {
    remove("shop.txt");
    cout << "\t\t\t\t\t\tThis File Is Deleted Successfully :)\n";
    cout << "\t\t\t\t\t\tMake sure Doing New File To Save All Info BEST WISHES\n\t\t\t\t\t\t :)\n";
    form_txt();
}
void edit() {
    int x = 0;
    string code;
    string name_product;
    string price;
    string quantity;
    string sales;
    string code1;
    string name_product1;
    string price1;
    string quantity1;
    string sales1;
    string par;
    cout << "\t\t\t\t\t\tWarning !!!!!!!!!!!\n\t\t\t\t\t\tIf there more code for product will Edit All !!!!!\n";
    cout << "\t\t\t\t\t\tEnter Code Of Product To Edit : ";
    cin >> par;
    ifstream infile;
    infile.open("shop.txt", ios::in | ios::binary);
    ofstream outfile;
    outfile.open("shop1.txt", ios::out | ios::binary);
    while (!infile.eof())
    {
        infile >> code;
        infile >> name_product;
        infile >> price;
        infile >> quantity;
        infile >> sales;
        if (!infile)break;
        if (code == par) {
            x = 1;
            cout << "\t\t\t\t\t\tEnter New Code of product : ";
            cin >> code1;
            cout << "\n\t\t\t\t\t\tEnter New name of product : ";
            cin >> name_product1;
            cout << "\n\t\t\t\t\t\tEnter New price of product : ";
            cin >> price1;
            cout << "\n\t\t\t\t\t\tEnter New quantity of product : ";
            cin >> quantity1;
            cout << "\n\t\t\t\t\t\tEnter New sales of product : ";
            cin >> sales1;
            code = code1;
            name_product = name_product1;
            price = price1;
            quantity = quantity1;
            sales = sales1;
        }
        outfile << code << "\t" << name_product << "\t\t" << price << "\t" << quantity << "\t\t" << sales << "\n";
    }
    if(x==1)
    cout << "\t\t\t\t\t\tThis Product Is Edited Successfully :)\n";
    else cout << "\t\t\t\t\t\tCode Is Not Found :<\n";
    infile.close();
    outfile.close();

    remove("shop.txt");
    rename("shop1.txt", "shop.txt");
}
void close_prog() {
    exit(0);
}
void choice() {
    int x;
    cout << "\t\t\t\t\t\tShop Management System\n";
    cout << "\t\t\t\t\t\t----------------------\n\n";
    cout << "\t\t\t\t\t\t 1. Add Product\n";
    cout << "\t\t\t\t\t\t 2. Edit Product\n";
    cout << "\t\t\t\t\t\t 3. Delete Product\n";
    cout << "\t\t\t\t\t\t 4. View Product and Sales\n";
    cout << "\t\t\t\t\t\t 5. Close\n";
    cout << "\t\t\t\t\t\t Enter your choice : ";
    cin >> x;
    cout << "\n\n";
    while (x) {
        switch (x)
        {
        case 1: {
            int y;
            cout << "\t\t\t\t\t\t 1.Add\n";
            cout << "\t\t\t\t\t\t 2.Return\n";
            cout << "\t\t\t\t\t\t 3.Close\n";
            cout << "\t\t\t\t\t\t Enter your choice : ";
            cin >> y;
            if (y == 1) { add(); }
            else if (y == 2) { choice(); }
            else if (y == 3) { close_prog(); }
            else cout << "\t\t\t\t\t\t Error\n\t\t\t\t\t\tEnter your choice again : \n";
            break; }
        case 2: {
            int y;
            cout << "\t\t\t\t\t\t 1.Edit\n";
            cout << "\t\t\t\t\t\t 2.Return\n";
            cout << "\t\t\t\t\t\t 3.Close\n";
            cout << "\t\t\t\t\t\t Enter your choice : ";
            cin >> y;
            if (y == 1) { edit(); }
            else if (y == 2) { choice(); }
            else if (y == 3) { close_prog(); }
            else cout << "\t\t\t\t\t\t Error\n\t\t\t\t\t\tEnter your choice again : \n";
            break; }
        case 3: {
            int y;
            cout << "\t\t\t\t\t\t 1.Delete\n";
            cout << "\t\t\t\t\t\t 2.Delete All\n";
            cout << "\t\t\t\t\t\t 3.Return\n";
            cout << "\t\t\t\t\t\t 4.Close\n";
            cout << "\t\t\t\t\t\t Enter your choice : ";
            cin >> y;
            if (y == 1) { del(); }
            else if (y == 2) { del_all(); }
            else if (y == 3) { choice(); }
            else if (y == 4) { close_prog(); }
            else cout << "\t\t\t\t\t\t Error\n\t\t\t\t\t\tEnter your choice again : \n";
            break; }
        case 4: {
            int y;
            cout << "\t\t\t\t\t\t 1.View All Data\n";
            cout << "\t\t\t\t\t\t 2.Return\n";
            cout << "\t\t\t\t\t\t 3.Close\n";
            cout << "\t\t\t\t\t\t Enter your choice : ";
            cin >> y;
            if (y == 1) { view(); }
            else if (y == 2) { choice(); }
            else if (y == 3) { close_prog(); }
            else cout << "\t\t\t\t\t\t Error\n\t\t\t\t\t\tEnter your choice again : \n";
            break; }
        case 5:close_prog(); break;
        default: {

            cout << "\t\t\t\t\t\t\tError!!!!!!!\n\t\t\t\t\t\t Please Enter Right Number \n";
            choice();

        }
        }
    }
}

int main()
{
    form_txt();
    choice();
    
    return 0;
}