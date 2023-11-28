#include <iostream> 
#include <fstream>

using namespace std;

void checkValidInput() {
    if (cin.fail()) {
        throw "Wrong data";
    }
}

void checkValidParams(double& x, double& b, double& h, int& n) {
    if (b < x || h < 0 || n < 2) {
        throw "Incorrect value";

    }
}

double calculate(double x, int n) {

    double y;

    if (x <= 0) {

        y = 0;

        for (int i = 0; i < n; i++) {

            double sum = 0;

            for (int j = 0; j < n; j++) {
                double term = x - j + x * j;

                if (term) {
                    sum += 1 / term;
                }

            }
            y += sum;
        }
    }
    else {
        y = 1;
        for (int i = 1; i < n; i++) {
            y *= 1 / x - 1 / i;
        }

    }
    return y;
}

void calculate_in_a_loop(double x, double b, double h, int n, bool stream) {
    ofstream fout("file.txt");
    while (x <= b) {
        if (stream) {
            fout << "y = " << calculate(x, n) << endl;
            fout << "x = " << calculate(x, n) << endl;
        }
        cout << "y = " << calculate(x, n) << endl;
        cout << "x = " << x << endl;
        x += h;
    }

}

int main() {
    setlocale(LC_ALL, "RU");

    double a;
    double b;
    double h;
    int n;
    bool stream;

    try {
        cout << "Введите a: "; cin >> a;
        cout << "Введите b: "; cin >> b;
        cout << "Введите h: "; cin >> h;
        cout << "Введите n: "; cin >> n;
        cout << "Желаете записать в файл ? (1/0)"; cin >> stream;
        checkValidInput();
        calculate_in_a_loop(a, b, h, n, stream);
    }
    catch (const char ex) {
        cout << ex << endl;
        return -1;
    }
    catch (...) {
        cout << "Unknown error" << endl;
        return -2;
    }

}
