# Overloading-Operators
C++
//Objective:to practice operator-overloading


#include <iostream>
#include <stdlib.h>
#include <cmath>
using namespace std;

class Complex
{
public:
	Complex(float=1.0,float=1.0);
	void set_real_and_imag (float, float);
	void print_complex();
	void print_magnitude();  //Print the Magnitude of the Complex number.

	float get_magnitude();

    friend Complex operator+(const Complex& c1, const Complex& c2);
    friend Complex operator-(const Complex& c1, const Complex& c2);
    friend Complex operator*(const Complex& c1, const Complex& c2);
    friend Complex operator/(const Complex& c1, const Complex& c2);
    friend bool operator!=(const Complex& c1, const Complex& c2);
    friend bool operator==(const Complex& c1, const Complex& c2);
    friend bool operator>(const Complex& c1, const Complex& c2);
    friend bool operator<(const Complex& c1, const Complex& c2);

    //Complex operator*(const Complex)

	friend ostream &operator<<(ostream &, Complex &);
	friend istream &operator>>(istream &, Complex &);
  // CAN You OVERLOAD AN OPERATOR USING "friend" keyword ????

private:
	float real;       //Real part
	float imaginary;  //Imaginary part
	float calculate_magnitude();   //Returns the magnitude of the Complex number

};

float Complex::calculate_magnitude()
{
    return sqrt(real*real + imaginary*imaginary);
}

float Complex::get_magnitude()
{
    return calculate_magnitude();
}

void Complex::print_magnitude()
{
    cout << "The magnitude of this complex number is " << get_magnitude();
}

/*--------------------------------------------------------*/

Complex::Complex(float m, float n)
{
	set_real_and_imag(m,n);
}

/*--------------------------------------------------------*/

void Complex::set_real_and_imag(float x, float y)
{

	real = x;
	imaginary = y;

}

/*--------------------------------------------------------*/

void Complex::print_complex()
{
	cout<<real<<" + j"<<imaginary<<endl;
}

/*--------------------------------------------------------*/

ostream &operator<<(ostream &output, Complex &object)
{
	output<<object.real<<" + j"<<object.imaginary<<endl;
	return output;
}

/*--------------------------------------------------------*/

istream &operator>>(istream &input, Complex &object)
{
	cout<<"Enter real, imaginary:"<<endl;
	input>>object.real;
	input>>object.imaginary;
	return input;
}

Complex operator +(const Complex& complex1, const Complex& complex2)
{
    Complex temp;
    temp.real = complex1.real + complex2.real;
    temp.imaginary = complex1.imaginary + complex2.imaginary;
    return temp;
}

Complex operator -(const Complex& complex1, const Complex& complex2)
{
    Complex temp;
    temp.real = complex1.real - complex2.real;
    temp.imaginary = complex1.imaginary - complex2.imaginary;
    return temp;
}

Complex operator *(const Complex& complex1, const Complex& complex2)
{
    Complex temp;
    temp.real = complex1.real*complex2.real - complex1.imaginary*complex2.imaginary;
    temp.imaginary = complex1.real*complex2.imaginary + complex1.imaginary*complex2.real;
    return temp;
}

Complex operator /(const Complex& complex1, const Complex& complex2)
{
    Complex temp;
    temp.real = (complex1.real*complex2.real + complex1.imaginary*complex2.imaginary)/(complex2.real*complex2.real + complex2.imaginary*complex2.imaginary);
    temp.imaginary = (complex1.imaginary*complex2.real - complex1.real*complex2.imaginary)/(complex2.real*complex2.real + complex2.imaginary*complex2.imaginary);
    return temp;
}

bool operator !=(const Complex& complex1, const Complex& complex2)
{
    return (complex1.real != complex2.real && complex1.imaginary != complex2.imaginary);
}

bool operator ==(const Complex& complex1, const Complex& complex2)
{
    return(complex1.real == complex2.real && complex1.imaginary == complex2.imaginary);
}

bool operator >(const Complex& complex1, const Complex& complex2)
{
    return(sqrt(complex1.real*complex1.real + complex1.imaginary*complex1.imaginary) > sqrt(complex2.real*complex2.real + complex2.imaginary*complex2.imaginary));
}

bool operator <(const Complex& complex1, const Complex& complex2)
{
    return(sqrt(complex1.real*complex1.real + complex1.imaginary*complex1.imaginary) < sqrt(complex2.real*complex2.real + complex2.imaginary*complex2.imaginary));
}



/*--------------------------------------------------------*/

int main()
{
	Complex x(3,4),y(3,4),z1,z2,z3,z4;
	cout<<"x=";
	x.print_complex();
	x.print_magnitude();
	cout<<"y=";
	y.print_complex();
	y.print_magnitude();

	// Complex Numbers  k & l are of Class type Complex
	Complex k(1,1),l(1,1),z6,z7,z8,z9,z10;
	cin>>k>>l; // Input two Complex numbers k and l  , where k = 3 + j4 and l = 4 + j5
	if(k==l) // You need to define '==' operation for this line to work
	{cout<<"These 2 complex numbers are equal."<<endl;}
	if(k!=l) // You need to define '!=' operation for this line to work
	{cout<<"These 2 complex numbers are not equal."<<endl;}
    if(k>l) // You need to define '>' operation for this line to work
	{cout<<"k is bigger than l."<<endl;}
	if(k<l) // You need to define '<' operation for this line to work
	{cout<<"k is smaller than l."<<endl;}
	z6=k+l; // You need to define '+' operation for this line to work
	z7=k-l; // You need to define '-' operation for this line to work
	z8=k*l; // You need to define '*' operation for this line to work
	z9=k/l; // You need to define '=' operation for this line to work

	cout<<"z6="<<z6<<"z7="<<z7<<"z8="<<z8<<"z9="<<z9;
	cout<<"k="<<k<<"l="<<l;

	return(0);
}

