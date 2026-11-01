#include <iostream>
#include <string>
#include <iomanip>

class Vehicle {
private:
    int vehicleID;
    std::string vehicleType;
    int entryTime;
    int parkingDuration;
    double parkingFee;
    bool isOccupied;

public:
    Vehicle() {
        vehicleID = 0;
        vehicleType = "";
        entryTime = 0;
        parkingDuration = 0;
        parkingFee = 0.0;
        isOccupied = false;
    }

    Vehicle(int id, std::string type, int time, int duration) {
        vehicleID = id;
        vehicleType = type;
        entryTime = time;
        parkingDuration = duration;
        isOccupied = true;
        calculateFee();
    }

    int getVehicleID() { return vehicleID; }
    std::string getVehicleType() { return vehicleType; }
    int getEntryTime() { return entryTime; }
    int getParkingDuration() { return parkingDuration; }
    double getParkingFee() { return parkingFee; }
    bool getIsOccupied() { return isOccupied; }

    void setVehicleID(int id) { vehicleID = id; }
    void setVehicleType(std::string type) { vehicleType = type; }
    void setEntryTime(int time) { entryTime = time; }
    void setParkingDuration(int duration) { parkingDuration = duration; }
    void setParkingFee(double fee) { parkingFee = fee; }
    void setIsOccupied(bool occupied) { isOccupied = occupied; }

    void calculateFee() {
        if (!isOccupied) {
            parkingFee = 0.0;
            return;
        }

        double baseRate = 0.0;
        if (vehicleType == "Car" || vehicleType == "car" || vehicleType == "CAR") baseRate = 6.0;
        else if (vehicleType == "Motorcycle" || vehicleType == "motorcycle" || vehicleType == "MOTORCYCLE") baseRate = 4.0;
        else if (vehicleType == "Bicycle" || vehicleType == "bicycle" || vehicleType == "BICYCLE") baseRate = 2.0;

        bool isPeak = (entryTime >= 6 && entryTime <= 9) || (entryTime >= 15 && entryTime <= 18);

        double rateFirst2Hours = 0.0;
        if (isPeak) {
            rateFirst2Hours = baseRate * 1.30;
        } else {
            rateFirst2Hours = baseRate * 0.95;
        }

        double rateFromHour3 = baseRate * 0.90
