#include <iostream>
#include <fstream>
#include <map>
#include <sstream>
#include <string>
#include <iomanip>
#include <stdlib.h>

using namespace std;

class Record {
    string name;
    int code;
    double cost;
public:
    Record() {
    }
    Record(string tname,int tcode,double tcost) : name(tname),code(tcode),cost(tcost) { 
    }
    friend ostream& operator<< (ostream &os, const Record& r);
};

//print function
ostream& operator<< (ostream &os, const Record& r) {
    os << setw(10) << r.name << " " << setw(5) << r.code << " $"  << setw(10) << setprecision(2) << fixed << r.cost ;
    return os;
}

int main() {
    std::map<int, Record> myMap;
    ifstream data;
    size_t offset_count = 0;
    data.open("p5.txt");
    ofstream outFile("pi5.txt", ios::out);

    //if file can't be opened, exit
    if(!data) {
        cerr << "Open Failure" << endl;
        exit(1);
    }

    std::string line;
    while (std::getline(data, line)) {
        stringstream ss(line);
        int key;
        string name;
        int code;
        double cost;

        if(ss >> key >> name >> code >> cost) {
            Record r(name,code,cost);
            myMap.insert( pair<int,Record>(key,r));
        }
        else {
             cout << "Error";
        }
    }

    // print what's stored in map
    for(std::map<int,Record>::iterator x = myMap.begin(); x!=myMap.end(); ++x) {
        cout << setw(10) << x->first << ": " << x->second << endl;
    }
}   
