#include <iostream>
#include <sstream>
#include <string>
#include <iomanip>
using namespace std;

class Grocerycounter {
    private: 
        int counter;
        int overflow;
        int underflow;

        void increment(int amount) {
            counter += amount;

            if (counter > 9999) {
                counter -= 10000;
                overflow++;
            }
        }
        void decrement(int amount) {
            counter -= amount;

            if (counter < 0) {
                counter += 10000;
                underflow++;
            }
        }
    public:
        Grocerycounter() {
            counter = 0;
            overflow = 0;
            underflow = 0;
    }
        void incrementtens() {
            increment(1000);
    }
        void incrementones() {
            increment(100);
    }
        void incrementtenths() {
            increment(10);
    }
        void incrementhundredths() {
            increment(1);
    }
        void decrementtens(){
            decrement(1000);
        }
        void decrementones() {
            decrement(100);
        }
        void decrementtenths() {
            decrement(10);
        }
        void decrementhundredths() {
            decrement(1);
        }
        int overflows() {
            return overflow;
        }
        int underflows() {
            return underflow;
        }
        string total() {
            stringstream money;
            money << fixed << setprecision(2) << "$" << counter/100.0;
            return money.str();
        }
        void clear() {
            counter=0;
            overflow=0;
            underflow = 0;
    }
};

int main() {
    Grocerycounter count;

    count.incrementtens();
    count.incrementtenths();
    count.incrementtenths();
    count.incrementhundredths();
    count.incrementhundredths();
    count.incrementhundredths();

    cout << "Current Amount: " << count.total() << endl;

    count.decrementhundredths();

    cout << "Decremented Amount: " << count.total() << endl;
    cout << "Overflows: " << count.overflows() << endl;

    count.clear();
    
    cout << "Cleared" << endl;
    cout << count.total() << endl;
    cout << "Overflows: " << count.overflows() << endl;

    return 0;
}
