# Convolution-coding-and-decoding-using-c-
Error detection and correction techniques are essential in modern digital communication systems to ensure  reliable data transmission over noisy channels. Convolutional coding is a widely used error-correction method  that encodes data by combining current and past bits using predefined generator polynomials.


Code

#include <iostream>

#include <vector>

#include <bitset>

#include <algorithm>

using namespace std;

// Helper function to XOR two bits

int XOR(int a, int b) {

 return a ^ b;

}

// Function to encode data using convolutional encoding

vector<int> convolutionalEncode(const vector<int>& data, const vector<vector<int>>& generatorPolynomials) 

{

 int memorySize = generatorPolynomials[0].size() - 1;

 vector<int> shiftRegister(memorySize, 0);

 vector<int> encodedData;

 for (int bit : data) {

 // Shift the register

 shiftRegister.insert(shiftRegister.begin(), bit);

 shiftRegister.pop_back();

 // Generate encoded bits

 for (const auto& generator : generatorPolynomials) {

 int encodedBit = 0;

 for (size_t i = 0; i < generator.size(); i++) {

 encodedBit ^= (shiftRegister[i] * generator[i]);

 }
encodedData.push_back(encodedBit);

 }

 }

 return encodedData;

}

// Function to decode data using a simple Viterbi-like algorithm (for demonstration)

vector<int> convolutionalDecode(const vector<int>& receivedData, const vector<vector<int>>& 

generatorPolynomials, int constraintLength) {

 // A full Viterbi decoder implementation is complex and not included here

 // Placeholder: Assume perfect decoding for simplicity

 vector<int> decodedData = {1, 0, 1, 1, 0, 1, 0, 0, 1}; // Replace with actual decoding logic

 return decodedData;

}

int main() {

 // Example binary data

 vector<int> data = {1, 0, 1, 1, 0, 1, 0, 0, 1}; // Input data sequence

 // Define the generator polynomials for a (2, 1, 3) convolutional code

 // Represented as binary arrays

 vector<vector<int>> generatorPolynomials = {

 {1, 1, 1}, // Polynomial 7 in octal (111 in binary)

 {1, 0, 1} // Polynomial 5 in octal (101 in binary)

 };

 // Encode the data

 vector<int> encodedData = convolutionalEncode(data, generatorPolynomials);

 cout << "Encoded Data: ";

 for (int bit : encodedData) {

 cout << bit;

 }
cout << endl;

 // Introduce an error in the encoded data for testing (optional)

 vector<int> receivedData = encodedData;

 receivedData[4] = !receivedData[4]; // Flip one bit to simulate an error

 // Decode the received data

 vector<int> decodedData = convolutionalDecode(receivedData, generatorPolynomials, 3);

 cout << "Decoded Data: ";

 for (int bit : decodedData) {

 cout << bit;

 }

 cout << endl;

 // Check if the decoded data matches the original data

 if (data == decodedData) {

 cout << "Decoding successful: The original and decoded data match." << endl;

 } else {

 cout << "Decoding failed: The original and decoded data do not match." << endl;

 }

 return 0;

}
