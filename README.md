# update-carwash-2
// Float Charters 
// This program calculates total sale price for a customer shopping at car wash
#include <iostream>
#include <fstream>
#include <vector>
using namespace std;

//global declaration statements
void totalPrice(double &total);
double add(int);
//array which stores prices for services
double prices[2][4]= {{8.99, 14.99, 18.99, 22.99 }, { 1.50, 5.00, 10.00, 30.00 }};
double choices;
string UsrName[100] = {};
int idNum[100] = {};
int LogReg = 0;
int id = 0;
int size = 3;

void getinfo()
{
  string str;
  int i = 0;
  int j = 0;
  int k = 0;
  ifstream in;
  in.open("data.txt");
  while (getline(in, str))
  {
    if (i%2 == 0)
      UsrName[j++] = str;
    else 
      idNum[k++] = stoi(str);
    ++i;
  }
  in.close();
}

void selection_sort(string array1[],int array2[], int n)
{
  for(int i = 0; i < n; i++ )
  {
  int iMin = i;
  for (int j = i + 1; j < n; j++ )
    {
      if (array1[iMin] > array1[j])
      iMin = j;
    }
  string temp = array1[i];
  array1[i] = array1[iMin];
  array1[iMin] = temp;
  int temps = array2[i];
  array2[i] = array2[iMin];
  array2[iMin] = temps;
  }
}

int linear_search(int arr[], int n, int srch)
{
  for (int i = 0; i < n; i++)
  {
    if(arr[i] == srch)
      return i;
  }
  return -1;
}
int main()
{
  // main declaration statements
	int choice = 0;
	double total = 0;
	double washes;
	int tempID = 0;
  int y = 0;
	
	getinfo();
	
  selection_sort(UsrName,idNum,size);

  ofstream out;
	out.open("receipt.txt");
  out << "     A1A Carwash" << endl;
  out << "9516 Snow Heights Cir NE\n Albuquerque, NM 87112" << endl << endl;

	// prints texts about the car wash to user
	cout << "\t\tWelcome to A1A car wash!" << endl << "\t'You've tried the rest, now try the best'" << endl << endl;
	cout << "To register enter 1. To log in enter 2: ";
	cin >> LogReg;
	if (LogReg == 1)
	{
	  cout << "Create username: ";
    cin >> UsrName[3];
    cout << "ID number is: ";
    idNum[3] = rand()%1000000 + 1;
    cout << idNum[3];
    selection_sort(UsrName,idNum,size);
	}
  else if (LogReg == 2)
  {
    cout << "Enter id number: ";
    cin >> tempID;
    int y = linear_search(idNum,size,tempID);
    cout << y;
    if(y == -1)
    {
      cout << "\nUser not found!";
      exit(0);
    }
  }
  else 
  {
    cout << "Invalid input!";
    exit(0);
  }

  cout << "\nWelcome " << UsrName[y] << ",";
	cout << "\nOur custom washes are listed below\n";
	cout << "------------------------------------\n";
  // Display options 1-4
	cout << "1.Bronze\t\t$" << prices[0][0] << endl;
	cout << "2.Sliver\t\t$" << prices[0][1] << endl;
	cout << "3.Gold  \t\t$" << prices[0][2] << endl;
	cout << "4.Platinum\t\t$" << prices[0][3] << endl << endl;
		cout << "First off, How many cars will we be servicing today? ";
		cin >> washes;
    out << washes << "x";
		cout << "Great! What will your choice of wash be today?\n (Select options 1 - 4): ";
		cin >> choice;
		//Switch statement uses the input to then use other functions to sum the total
		switch (choice)
		{
		case 1:
			cout << "\nBronze selected\nThis package includes:\n*Deluxe Wash\n*Tire Clean\n" << endl;
      out << "Bronze  \t@$" << prices[0][0] << "\t\t$" << prices[0][0] * washes << endl;
			total += prices[0][0] * washes;
			total += add(choices);
			cout << "The total price comes out too : $" << total << endl;
			break;
		case 2:
			cout << "\nSilver selected\nThis package includes:\n*Deluxe Wash\n*Tire Clean\n*Interior Vacumm\n" << endl;
      out << "Silver  \t@$" << prices[0][1] << "\t\t$" << prices[0][1] * washes << endl;
			total += prices[0][1] * washes;
			total += add(choices);
			cout << "The total price comes out to : $" << total << endl;
			break;
		case 3:
			cout << "\nGold selected\nThis package includes:\n*Deluxe Wash\n*Tire Clean\n*Interior Vacumm\n*Coat Wax\n" << endl;
      out << "Gold    \t@$" << prices[0][2] << "\t\t$" << prices[0][2] * washes << endl;
			total += prices[0][2] * washes;
			total += add(choices);
			cout << "The total price comes out to : $" << total << endl;
			break;
		case 4:
			cout << "\nPlatinum selected\nThis package includes:\n*Deluxe Wash\n*Interior Vacumm\n*Coat Wax\n*Tire Shine\n*Complete Surface Protectant\n" << endl;
      out << "Platinum\t@$" << prices[0][3] << "\t\t$" << prices[0][3] * washes << endl;
			total += prices[0][3] * washes;
			total += add(choices);
			cout << "The total price comes out too : $" << total << endl;
			break;
		default:
			cout << "Invalid input select options 1-4" << endl;
		}
		//output total to receipt.txt file 


		out << "\ntotal: \t\t\t\t\t\t\t\t$" << total;
		out.close();
}

// This function adds choices for additional prices to total
double add(int choices)
{
    double total = 0;
		while(true)
		{
		  // Display texts and prices for additional features user to select 1-5
		  cout << "Would you like any additional services?\n";
  		cout << "---------------------------------------\n";
  		cout << "1. Air Freshener              $1.50\n";
  		cout << "2. Tire Pump                  $5.00\n";
  		cout << "3. Rotation of Tires          $10.00\n";
  		cout << "4. Oil Change plus Filter     $30.00\n";
  		cout << "5. No additional services\n";
  		cin >> choices;
  		//if else loop which runs when user inputs numbers 1-4 and ends with 5 when user no longer wants to add anymore features
		  if(choices == 1)
		  {
		    cout << "'Air Freshner added'" << endl;
  			cout << "An additional $1.50 will be charged." << endl;
  			total += prices[1][0];
		  }
		  else if (choices == 2)
		  {
		    cout << "'Tire Pump added'" << endl;
  			cout << "An additional $5.00  will be charged\n" << endl;
  			total += prices[1][1];
		  }
		  else if (choices == 3)
		  {
		    cout << "'Rotation of Tires added'" << endl;
  			cout << "An additional $10.00 will be charged\n" << endl;
  			total += prices[1][2];
		  }
		  else if (choices == 4)
		  {
		    cout << "'Oil Change added'" << endl;
  			cout << "An additional $30.00 will be charged\n" << endl;
  			total += prices[1][3];
		  }
		  else if (choices == 5)
		  {
		    break;
		  }
		  else
		  {
		    cout << "Please enter a number 1 - 5\n";
		  }

		}
		return total;
}









