#include <iostream>
#include <ctime>
#include <map>
#include <algorithm>
#include <sstream>
#include <unistd.h> // For Unix-based systems
#ifdef _WIN32
#include <windows.h> // For Windows
#endif

using namespace std;

void sleep_seconds(int seconds) {
#ifdef _WIN32
    Sleep(seconds * 1000); // Sleep function in Windows takes milliseconds
#else
    sleep(seconds); // Sleep function in Unix-based systems takes seconds
#endif
}

int main() {
    string userName;
    int birthYear, birthDay;
    string birthMonthStr;
    int birthMonth = 0;

    // Month map initialization
    map<string, int> monthMap;
    monthMap["january"] = 1; monthMap["jan"] = 1;
    monthMap["february"] = 2; monthMap["feb"] = 2;
    monthMap["march"] = 3; monthMap["mar"] = 3;
    monthMap["april"] = 4; monthMap["apr"] = 4;
    monthMap["may"] = 5;
    monthMap["june"] = 6; monthMap["jun"] = 6;
    monthMap["july"] = 7; monthMap["jul"] = 7;
    monthMap["august"] = 8; monthMap["aug"] = 8;
    monthMap["september"] = 9; monthMap["sep"] = 9;
    monthMap["october"] = 10; monthMap["oct"] = 10;
    monthMap["november"] = 11; monthMap["nov"] = 11;
    monthMap["december"] = 12; monthMap["dec"] = 12;

    cout << "Enter your name: ";
    getline(cin, userName);

    cout << "Enter your birth year: ";
    cin >> birthYear;

    cout << "Enter your birth month (name, short form, or number): ";
    cin >> birthMonthStr;

    // Convert input to lowercase
    transform(birthMonthStr.begin(), birthMonthStr.end(), birthMonthStr.begin(), ::tolower);

    // Determine the birth month
    if (isdigit(birthMonthStr[0])) {
        stringstream ss(birthMonthStr);
        ss >> birthMonth;
        if (birthMonth < 1 || birthMonth > 12) {
            cout << "Invalid month number entered." << endl;
            return 1;
        }
    } else if (monthMap.find(birthMonthStr) != monthMap.end()) {
        birthMonth = monthMap[birthMonthStr];
    } else {
        cout << "Invalid month entered." << endl;
        return 1;
    }

    cout << "Enter your birth day: ";
    cin >> birthDay;

    while (true) {
        time_t t = time(0);
        tm* now = localtime(&t);
        int currentYear = now->tm_year + 1900;
        int currentMonth = now->tm_mon + 1;
        int currentDay = now->tm_mday;
        int currentHour = now->tm_hour;
        int currentMinute = now->tm_min;
        int currentSecond = now->tm_sec;

        // Clear screen for Unix-based systems and Windows
        #ifdef _WIN32
            system("cls");
        #else
            system("clear");
        #endif

        // Display current date and time
        cout << "Current date and time: " << currentYear << "-" << currentMonth << "-" << currentDay
             << " " << (currentHour < 10 ? "0" : "") << currentHour << ":"
             << (currentMinute < 10 ? "0" : "") << currentMinute << ":"
             << (currentSecond < 10 ? "0" : "") << currentSecond << endl;

        // Calculate age
        int ageYears = currentYear - birthYear;
        int ageMonths = currentMonth - birthMonth;
        int ageDays = currentDay - birthDay;

        if (ageDays < 0) {
            ageMonths--;
            // Determine days in the previous month
            int daysInPrevMonth = 30;
            if (birthMonth == 2) {
                daysInPrevMonth = 28;
                if ((birthYear % 4 == 0 && birthYear % 100 != 0) || (birthYear % 400 == 0)) {
                    daysInPrevMonth = 29;
                }
            } else if (birthMonth == 4 || birthMonth == 6 || birthMonth == 9 || birthMonth == 11) {
                daysInPrevMonth = 30;
            } else {
                daysInPrevMonth = 31;
            }
            ageDays += daysInPrevMonth;
        }

        if (ageMonths < 0) {
            ageYears--;
            ageMonths += 12;
        }

        // Display age
        cout << userName << ", you are " << ageYears << " years, " << ageMonths << " months, and " << ageDays << " days old." << endl;

        // Wait for 1 second before updating
        sleep_seconds(1);
    }

    return 0;
}
