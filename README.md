# Assignment-2-Q1-of-oop
This is question 1 of my 2nd assingnment for oop that creates a class stores a day dynamically and returns next day and previous day by using all concepts of oops coverd so far
#include<iostream>
using namespace std;
class daytype{
	private:
		string *day;//it is pointer to dynamic allocation
		static const string week[7];//static means it belongs to class itself and shared by all instactces 
		public:
			daytype(const string day_a){
				day=new string(day_a);//dynamically allocates memory to day
				
			}
			~daytype(){
		delete day;//destructor
	}
			void setday(const string& day_a){
				*day=day_a;//sets the day by accepting the refrence of day_a and storing it in day
			}
			string& getday()const{
				return *day;//this func return the refrence of type string and it is const as it
				//doenst modify any memebr of class specifically day variable
			}
			string getnextday() const{//returns the next day.
//days of week
				static const string week[7]={"sunday","Monday","tuesday","wednesday","thursday","friday","saturday"};
				int index;
				for (int i = 0; i < 7; ++i) {
				//checks among these days of week which day was called in day and stores its index
            if (*day == week[i]) {
                index = i;
                break;
            }
        }//since next day is reuired so add 1 in current day
        int newday=index+1;
        return week[newday% 7];
			}
			string getPreviousDay() const {//return previous day
        static const string week[7]={"sunday","Monday","tuesday","wednesday","thursday","friday","saturday"};
        int index;
        for (int i = 0; i < 7; ++i) {
            if (*day == week[i]) {
                index = i;
                break;
            }
        }
        int prevday=index-1;
        return week[prevday% 7];
    }
    daytype(const daytype &obj){//deep copying is used here
    	day=new string(*obj.day);
    }
	
};
int main(){
	daytype today("sunday");
	cout<<"Today is : "<<today.getday()<<endl;
	cout<<"next day is : "<<today.getnextday()<<endl;
	cout<<"previous day is : "<<today.getPreviousDay()<<endl;
	daytype exam(today);
	cout<<"Exam day is: "<<exam.getday()<<endl;
	cout<<"Day next to Exam day is: "<<exam.getnextday()<<endl;
	cout<<"previous day to Exam day is: "<<exam.getPreviousDay()<<endl;
	}
