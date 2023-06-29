

# QCG - Open Project 2023 : Building a basic Quantum Adder using Toffoli Gates


By Aarav Ratra

Enrolment No.: 21122002

Branch: EPh 2021-25

  
## Problem Statement
Alice wishes to perform the addition of two 4-bit numbers using Quantum Circuits.
Let those two numbers be a and b.

<img width="276" alt="image" src="https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/4432e1a5-9d43-4a52-8766-a4203f3edf1c">


In classical digital electronics, this is achieved using the full-adder circuit, which inputs the bits a_i,b_i and carry bit C_(i-1) and returns the sum bit S_i and carry bit C_i. Hence, the result of the computation would be as follows: 

<img width="386" alt="image" src="https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/20dc074a-6f9c-4df5-a101-b8309b69572a">

Your task is to help Alice design a fully functional Quantum Adder using just CNOT and Toffoli Gates. 

## Step 1: Designing a single full adder circuit

The relations are given as follows:

S(i) = a(i)⊕b(i)⊕C(i-1)

C(i) = a(i)b(i)⊕(a(i)⊕b(i))C(i-1) 

Since a generalised toffoli gate can encompass all classical boolean gate operations (AND,OR,NOT,XOR) , we can design the circuits using just CX and CCX gates. The full adder circuit is a 4 qubit circut and has the following inputs:

<img width="382" alt="image" src="https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/804eed3b-518b-4c26-9d2a-987fa66e9663">

*(Image referred from the problem statement)*

Here is the thinking I have used to design the circuit:

1. a(i)b(i) is found to be one of the terms of the carry bit C(i) and is XOR-ed with another quantity. Hence, a toffoli gate is used on C(i) (initialised to |0>) with a(i) and b(i) as control qubits. Note that whenever we need an AND boolean relationship, using a CCX gate would be the right direction. 

2. The quantity a(i)⊕b(i) is central to both the S(i) bit as well as the C(i) bit. Hence our next step would be to use a CX gate to generate a(i)⊕b(i) by using b(i) as the target qubit. 

3. Now, we can easily obtain the required state for C(i) by using a Toffoli with the control bits being the C(i-1) bit and the a(i)⊕b(i) bit.

4. Our last step would be to correctly obtain the SUM bit. That can be obtaining using a simple CX with C(i-1) as our control bit.

The resulting circuit shall look like this. This is the single full adder.

![image](https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/d27f5854-8fbb-450e-84db-5cc64e01c213)

## Step 2: Designing a 4-Bit Quantum Adder using these Single Full Adders

Now, we shall design a 4-bit adder using the single full-adder circuit as a module for addition of each bit. All the carry bits (incl C(-1)) are initialised to 0 (by default).

<img width="556" alt="image" src="https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/ae8ec936-be35-4237-9189-9b66956dafd6">

I have followed the above skeleton (diagram referred from the problem statement) and used that. 

I have defined separate registers for the first bit, 2nd bit and the Carry Bits. For the sake of uniformity/convenience, I have used a separate register containing the C(-1) bit.

Will be defining a separate circuit for the Full Adder, and separate circuits for state initialization

## Results:
The given test cases have given satisfactory results:

### Test Case #1: A = |0010> , B = |1011>

![image](https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/8c3c0243-7040-4538-b622-a887d78da979)

### Test Case #2: A = |0001> , B = |0011>

![image](https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/18670727-7d2e-45b8-938a-1c501be21db2)

### Test Case #3: A = |0010>+|0100> / √2 , B = |1011> + |0001> /√2

![image](https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/b9e98e5b-f8c2-4f31-82e4-daa5901c7017)

### Test Case #4: A = |0000>+|0111> / √2 , B = |0111> + |1000> /√2

![image](https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/d694d982-ba31-4abb-91eb-b69940170b2a)

## Bonus Tasks:

I have attempted the first Bonus Task as well. 

### Bonus Task #1: If the qubits of registers A and B are entangled

In the above cases, it was clearly seen that Quantum Full Adders would work if the bits a and b were superpositions, hence can be used for finding all possible addition combinations.

Now, we shall see a case where the registers A and B are such that they are entangled. Will take a few test cases:

1. |a>|b> = (|0000>|0000> + |1111>|1111>)/√2
  Result:
  ![image](https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/309aebca-5308-4b5f-aaa6-86cc6e2f1b54)

2. |a>|b> = (|0101>|0101> + |1010>|1010>)/√2
   Result:
   ![image](https://github.com/aarav-rm8/QuantumFullAdder/assets/106330659/ada0dc4c-66b8-46b4-9ea1-a0612d0ce650)

#### Explanation

We can define our qubit inputs as

|a>|b> = ∑|a_k>|b_k> = |a_0>|b_0> + |a_1>|b_1> +...

On measurement, we obtain one of the |a_k>|b_k> values, hence when we do multiple shots of the same job we will get all the |a_k>|b_k> values.

In the case of un-entangled registers |a> and |b>, we could factor out |a> and |b> and hence instead of expressing as a sum ∑|a_k>|b_k>, we can instead refer to it as a product and hence use that to find all the possible summations for diff values of A and B (like solve for all possible combinations of A and B that can occur)

When the qubits are entangled, it becomes impossible to factor them as |a> and |b>. And hence we have to always look towards it as a SUM ∑|a_k>|b_k> instead. This would prove useful if we are tying to solve only specific combinations of A and B.

# THANK YOU





