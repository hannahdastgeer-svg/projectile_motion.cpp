#include <iostream>
#include <stdio.h>
#include <cmath>

using namespace std;

//macro
#define EPSILON 0.1 //margin of error 
#define dt 0.1 //sampling increment 
#define a1 -9.81 //upwards acceleration
#define a2 9.81 //downwards acceleration 

//define constants
double y_t = 0; double x_t = 0; const double pi = acos(-1); 

double UP_projectile(double v_0, double time_up, double angle){
    for (int t = 0; t <= 500; t++){
        //kinematic equation y_t = v_0*t + 1/2at^2 
        //modify time increments
        y_t = sin(angle)*v_0*(t*dt) + 0.5*t*t*dt*dt*a1;
        x_t = cos(angle)*v_0*(t*dt);
        cout << "time t: " << t*dt <<"s ";
        cout << "| y position: " << y_t <<"m ";
        cout << "| x position: " << x_t <<"m "<< endl;
        if (abs(t*dt - time_up) <= EPSILON){
            break;
        }
        if (t>=249){
            cout << "time too long, adjust values" << endl;
            break;
        }
    }
    cout << "max height: " << y_t << "m at time: " <<time_up <<"s" << endl;
    return y_t;
}

void DOWN_projectile(double v_0, double time_up, double angle, double y_max){
    for (int t = (int)(time_up); t <= 500; t++){
        //kinematic equation y_t = v_0*t + 1/2at^2 
        //modify time increments
        y_t = y_max - (0.5*t*t*dt*dt*a2);
        x_t = cos(angle)*v_0*(int)(time_up) +1.25+ cos(angle)*v_0*(t*dt);
        cout << "time t: " << t*dt+(int)(time_up)+dt <<"s";
        cout << "| y position: " << y_t <<"m ";
        cout << "| x position: " << x_t <<"m "<< endl;
        if (y_t <= EPSILON){
            break;
        }
        if (t>=249){
            cout << "time too long, adjust values" << endl;
            break;
        }
    }
    cout << "max distance: " << x_t << "m at time: " <<time_up*2.0 <<"s" << endl;
}

int main(){
    double v_0 = 25;
    double angle = pi/3;
    double time_up = -1*v_0*sin(angle)/a1;
    double y_max = UP_projectile(v_0, time_up, angle);
    DOWN_projectile(v_0, time_up, angle, y_max);
    // cout << cos(angle)*v_0*(time_up*dt) << endl;
    return 0;
}




