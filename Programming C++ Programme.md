#include <iostream>
#include <iomanip>
#include <string>

using namespace std;

const int CLOTHES_COUNT = 4;

struct ClothingItem {
    string name;
    double price;
};

void displayIntroduction() {
    cout << "----------------------------------------------\n";
    cout << "  Welcome to the Online Clothing Store System\n";
    cout << "----------------------------------------------\n\n";
    cout << "Project Title: Online Clothing Store System\n";
    cout << "Purpose      : To simulate an online shopping experience with item selection,\n\n";
    cout << "Developers   :\n";
    cout << " nawod taruka        ITBNM-2516-0020\n";
    cout << " hiranaya vichakshana ITBNM-2516-0013\n";
    cout << " nethmi kaushalaya   ITBNM-2516-0028\n";
    cout << " chathurada          ITBNM-2516-0045\n\n";
}

int main() {
    displayIntroduction();

    string customer;
    cout << "Enter your name: ";
    getline(cin, customer);

    ClothingItem clothes[CLOTHES_COUNT] = {
        {"T-Shirt", 1200.00},
        {"Jeans", 2500.00},
        {"Jacket", 3500.00},
        {"Shoes", 4000.00}
    };

    int quantity[CLOTHES_COUNT] = {0};

    cout << "\nWelcome to the Online Clothing Store, " << customer << "!\n";
    cout << "\n----- Available Items -----\n";
    for (int i = 0; i < CLOTHES_COUNT; i++) {
        cout << i + 1 << ". " << clothes[i].name
             << " - Rs. " << fixed << setprecision(2) << clothes[i].price << endl;
    }

    char more;
    int choice, qty;
    do {
        cout << "\nEnter item number to add to cart: ";
        cin >> choice;
        if (choice < 1 || choice > CLOTHES_COUNT) {
            cout << "Invalid choice. Try again.\n";
            continue;
        }
        cout << "Enter quantity: ";
        cin >> qty;
        quantity[choice - 1] += qty;
        cout << "Add more items? (y/n): ";
        cin >> more;
    } while (more == 'y' || more == 'Y');

    double subtotal = 0.0;
    cout << "\n--- Your Cart ---\n";
    for (int i = 0; i < CLOTHES_COUNT; i++) {
        if (quantity[i] > 0) {
            double itemTotal = clothes[i].price * quantity[i];
            subtotal += itemTotal;
            cout << clothes[i].name << " x " << quantity[i]
                 << " = Rs. " << fixed << setprecision(2) << itemTotal << endl;
        }
    }
    cout << "Subtotal: Rs. " << fixed << setprecision(2) << subtotal << endl;

    double discount = 0.0;
    if (subtotal >= 10000)
        discount = subtotal * 0.15;
    else if (subtotal >= 5000)
        discount = subtotal * 0.10;
    else if (subtotal >= 2000)
        discount = subtotal * 0.05;

    cout << "Discount Applied: Rs. " << fixed << setprecision(2) << discount << endl;

    string location;
    double shipping = 0.0;
    cout << "Enter your city for shipping: ";
    cin.ignore();
    getline(cin, location);

    if (location == "Colombo" || location == "colombo")
        shipping = 0.0;
    else
        shipping = 500.0;

    cout << "Shipping Cost: Rs. " << fixed << setprecision(2) << shipping << endl;

    int paymentChoice;
    cout << "\nSelect Payment Method:\n";
    cout << "1. Cash on Delivery\n2. Credit/Debit Card\n3. Online Banking\n";
    cout << "Enter your choice (1-3): ";
    cin >> paymentChoice;

    string paymentMethod;
    switch (paymentChoice) {
        case 1: paymentMethod = "Cash on Delivery"; break;
        case 2: paymentMethod = "Credit/Debit Card"; break;
        case 3: paymentMethod = "Online Banking"; break;
        default: paymentMethod = "Unknown"; break;
    }

    double total = subtotal - discount + shipping;

    cout << "\n===== Final Bill =====\n";
    cout << "Customer: " << customer << endl;
    cout << "Subtotal: Rs. " << fixed << setprecision(2) << subtotal << endl;
    cout << "Discount: Rs. " << fixed << setprecision(2) << discount << endl;
    cout << "Shipping: Rs. " << fixed << setprecision(2) << shipping << endl;
    cout << "Payment Method: " << paymentMethod << endl;
    cout << "----------------------\n";
    cout << "Total Amount Payable: Rs. " << fixed << setprecision(2) << total << endl;
    cout << "======================\n";

    return 0;
}