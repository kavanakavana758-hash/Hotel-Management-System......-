# Hotel-Management-System......-
#include <iostream>
#include <fstream>
#include <vector>
#include <string>
#include <iomanip>
#include <sstream>
#include <limits>

using namespace std;

// ========================= ROOM CLASS =========================
class Room {
private:
    int roomNumber;
    string roomType;
    double price;
    bool booked;
    int customerId;

public:
    Room() {
        roomNumber = 0;
        roomType = "";
        price = 0.0;
        booked = false;
        customerId = -1;
    }

    Room(int number, string type, double p) {
        roomNumber = number;
        roomType = type;
        price = p;
        booked = false;
        customerId = -1;
    }

    int getRoomNumber() const {
        return roomNumber;
    }

    string getRoomType() const {
        return roomType;
    }

    double getPrice() const {
        return price;
    }

    bool isBooked() const {
        return booked;
    }

    int getCustomerId() const {
        return customerId;
    }

    void bookRoom(int id) {
        booked = true;
        customerId = id;
    }

    void checkoutRoom() {
        booked = false;
        customerId = -1;
    }

    void display() const {
        cout << left
             << setw(12) << roomNumber
             << setw(15) << roomType
             << setw(12) << fixed << setprecision(2) << price
             << setw(15) << (booked ? "Booked" : "Available")
             << setw(12) << (booked ? to_string(customerId) : "-")
             << endl;
    }

    // Save room information into file
    void save(ofstream &file) const {
        file << roomNumber << "|"
             << roomType << "|"
             << price << "|"
             << booked << "|"
             << customerId << endl;
    }

    // Load room information from file
    void load(string line) {
        stringstream ss(line);
        string temp;

        getline(ss, temp, '|');
        roomNumber = stoi(temp);

        getline(ss, roomType, '|');

        getline(ss, temp, '|');
        price = stod(temp);

        getline(ss, temp, '|');
        booked = stoi(temp);

        getline(ss, temp, '|');
        customerId = stoi(temp);
    }
};


// ========================= CUSTOMER CLASS =========================
class Customer {
private:
    int customerId;
    string name;
    string phone;
    string address;
    int roomNumber;

public:
    Customer() {
        customerId = 0;
        name = "";
        phone = "";
        address = "";
        roomNumber = -1;
    }

    Customer(int id, string n, string p, string a, int room) {
        customerId = id;
        name = n;
        phone = p;
        address = a;
        roomNumber = room;
    }

    int getCustomerId() const {
        return customerId;
    }

    string getName() const {
        return name;
    }

    string getPhone() const {
        return phone;
    }

    string getAddress()