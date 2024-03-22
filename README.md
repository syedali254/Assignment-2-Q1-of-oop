# Assignment-2-Q1-of-oop
<br>
#include<iostream>
using namespace std;
class daytype{
	private:
		string *day;//it is pointer to dynamic allocation
		static const string week[7];//static means it belongs to class itself and shared by all instactces and const means it wont be modified
		public:
			daytype(const string day_a){
				day=new string(day_a);//dynamically allocates memory to day
				
			}
			~daytype(){
		delete day;//destructor
	}
			void setday(string& day_a){
				*day=day_a;//sets the day by accepting the refrence of day_a and storing it in day
			}
			string& getday()const{
				return *day;
				//this func return the refrence of type string and it is const as it
				//doenst modify any memebr of class specifically day variable and return as it is
			}
			string getnextday() const{//returns the next day.
//days of week
				
				int index;
				for (int i = 0; i < 7; ++i) {
				//checks among these days of week which day was called in day and saves its index
            if (*day == week[i]) {
                index = i;
                break;
            }
        }//since next day is reuired so add 1 in current day
        int newday=index+1;
        return week[newday% 7];
			}
			string getPreviousDay() const {//return previous day
        
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
    string getdayafter(int numofdays)const{
    	 
    	 int index;
    	 for(int i=0;i<7;i++){
    	 	if(*day==week[i]){
    	 		index=i;
    	 		break;
			 }
			 
		 }
		 int newday=index+numofdays;
		 return week[newday%7];
	}
    daytype(const daytype &obj){//deep copying is used here
    	day=new string(*obj.day);
    }
    void print() {
    	cout<<"Current Day is: "<<*day<<endl;
	}
	
	
};
//static members are initialized ousted class
const string daytype::week[7]={"Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"};

int main(){
	string starting_day;
	int choice;
	daytype *today=new daytype("Monday");//today is a pointer to class no the object itself

	do {
		cout << "\nMenu:\n";
		cout << "1. Set starting day\n";
		cout << "2. show current day\n";
		cout << "3. show next day\n";
		cout << "4. show previous day\n";
		cout << "5. show day after certain number of days\n";
		cout << "6. Exit\n";
		cout << "Enter your choice: ";
		cin >> choice;

		switch (choice) {
			case 1: {
				cout << "Enter starting day: ";
				cin >> starting_day;
				today->setday(starting_day);//this opearor is used because today is not object itself but the poinnter to daytype so -> is used to derefrence
				break;
			}
			case 2: {
				today->print();
				break;
			}
			case 3: {
				cout<<"Next day is:"<<today->getnextday()<<endl;
				break;
			}
			case 4: {
				cout<<"Previous day is: "<<today->getPreviousDay()<< endl;
				break;
			}
			case 5: {
				int adddays;
				cout<<"Enter number of days to add: ";
				cin>>adddays;
				cout<<"The day after "<<adddays<<"days is: "<<today->getdayafter(adddays)<<endl;
				break;
			}
			case 6: {
				cout<<"Exiting program."<<endl;
				break;
			}
			default: {
				cout<<"Invalid choice. Please try again." << endl;
			}
		}
	} while (choice != 6);

	return 0;
}
