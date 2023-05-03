Download Link: https://assignmentchef.com/product/solved-cs311-assignment-2
<br>
Write an assembler for the <em>ToyRISC </em>ISA.

<h2>Input to the Program</h2>

<ol>

 <li>full path to the assembly program.</li>

 <li>full path to the object file to be created.</li>

</ol>

<strong>Output of the Program</strong>

<ul>

 <li>the program must create the object file at the specified location.</li>

</ul>

<h2>Broad Outline of the Steps</h2>

The mechanism of assembly has already been discussed in class. As an example, consider the assembly of this instruction from assignment 1’s statement: load %x0, $a, %x4 in Table 1.

Table 1: Assembly of load %x0, $a, %x4

<table width="461">

 <tbody>

  <tr>

   <td width="75"><strong>Field</strong></td>

   <td width="53"><strong>Value</strong></td>

   <td width="333"><strong>Binary Representation</strong></td>

  </tr>

  <tr>

   <td width="75">Operation</td>

   <td width="53">load</td>

   <td width="333">10110</td>

  </tr>

  <tr>

   <td width="75">rs1</td>

   <td width="53">x0</td>

   <td width="333">00000</td>

  </tr>

  <tr>

   <td width="75">rd</td>

   <td width="53">x4</td>

   <td width="333">00100</td>

  </tr>

  <tr>

   <td width="75">imm</td>

   <td width="53">0</td>

   <td width="333">00000000000000000 (recall that ‘a’ refers to address 0)</td>

  </tr>

  <tr>

   <td colspan="2" width="128"><strong>Full Instruction</strong></td>

   <td width="333"><strong>10110000000010000000000000000000</strong>= <strong>-1341652992 </strong>(signed representation)</td>

  </tr>

 </tbody>

</table>

The task of assembly has been further simplified. We have done the parsing of the assembly program for you (git clone <a href="https://gitea.iitdh.ac.in:443/rajshekar.k/CS311_assignment2.git">https://gitea.iitdh.ac.in:</a>

<a href="https://gitea.iitdh.ac.in:443/rajshekar.k/CS311_assignment2.git">443/rajshekar.k/CS311_assignment2.git</a><a href="https://gitea.iitdh.ac.in:443/rajshekar.k/CS311_assignment2.git">)</a>.

<ul>

 <li>For all labels, both in data and in code, we have set up the symbol table that maps label to address. To get the address corresponding to a label str, simply call symtab.get(str).</li>

 <li>Similarly, instructions are also gathered in a simple array. To access the instruction at a given address addr, simply call getInstructionAt(addr).</li>

 <li>Each instruction is represented by an object of the Instruction class (see generic/Instruction). You can get the operation type and the operands by calling the appropriate functions mentioned in this class.</li>

 <li>Each operand is represented by an object of the Operand class (see generic/Operand). You can get (i) the operand type – that is, is it a register operand, an immediate, or a label, and (ii) the value – that is, the register number, the immediate value, or the label string.</li>

</ul>

You only need to complete the function src.generic.Simulator.simulate().

The expected format of the object file is as follows:

<ul>

 <li>Header: Here, you simply write the address of the first instruction. This is an integer, and therefore 4 bytes long.</li>

 <li>Data: Here, you write all the static data one after another. Each datum is 4 bytes long.</li>

 <li>Text: Here, you write the encoded instructions one after another. Each instruction is 4 bytes long.</li>

</ul>

Please see the following example:

. data a

10 b

20 . text

load %x0 , $a , %x4

end

The given assembly file will contain the integers (and not strings!) 2, 10, 20, −1341652992, −402653184. The header consists of the instruction of the first instruction, in this case 2. The two data follow. The binary equivalents of the load and end instructions are then placed.

You may read the file that you create using the xxd command.