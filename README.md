<div style="text-align:center">
  <img src="https://soliditylang.org/images/logo.svg" alt="Solidity Logo">
</div>

## Solidity Cheatsheet

This is The Complete Solidity Notes With Code Snippest and Comments, Which Will Help You Understand Better

---

Before Writing Solidity Code, We Have To Include This Code Snippest

```solidity
SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// 0.8.0 Refers to the Version of Solidty
```
---

*Lets Start*

&nbsp;

1. Data Types Values Types

```solidity
contract ValuesTypes {
    bool public Item = true;
    uint256 public UnsignedInt = 1000;  // We Can Set int#. Here Hash Represent Any Number. 0 to 2^#-1

    int256 public MyNum = 7000;  // We Can Set int#. Here Hash Represent Any Number. 0 to 2^#-1
    address public  MyAddress=0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;  //Sture 20 Bit Adress. Store Hex Adress

    bytes32 public  MyBytes32;
}

```
---
2. Solidity Functions

```solidity
contract FunctionsInSolidity{
    uint public Age=20;

    function Add(uint X, uint Y) public pure returns(uint) {
        return X+Y;
    }
    function GetAge() public view returns(uint) {
        return Age;
    }
    function ChangeAge() public {
        Age+=1;
    }
    function InternalFunction () internal {
        // Code
    }
}
function Outside(uint XYZ){
    // I Can Be Declared Outside the Contract But My Button Cannot be Shown While Deploy
}
```
---
3. State Variable

```solidity
contract StateVariable{
    /*
    In Solidity Variables are of 3 Types (State,Local,Global). But Today We Will Discuss Only State Variables
    State Variables are Those That Are Declared Inside Contract, But They are Outside of Functions.

    State Variables Are Important. Because They Cost Gas and They Are Directly Stored in Blockchain Storage. And There are only 3 Ways to
    Initialise Them. 1) By Directly Initialising While Declaring. 2) By Constructor. 3) By Using Function.
    */

    uint16 public MyStateVariable;

    // MyStateVariable=1500; This is Not Allowed and Will Give Error

    constructor(){
        MyStateVariable=2000;
    }
    function SetVariable() public {
        MyStateVariable=5000;
    }

}
```
---
4. Local Variable

```solidity
contract LocalVariable{

    /*
    Local Variable are Those That Are Declared or Intialized Inside Functions. They Stored Inside RAM and Have Short Life Span, Depends
    on Life Cycle of Function. They also Cost Gas, But Very Negligible
    */

    function DealLocalVariable() public pure returns (uint,bool) {
        uint Age=12;
        bool Status=false;

        Age=20;

        return (Age,Status);
    }
}
```
---
5. Global Variable

```solidity
contract GlobalVariable{
    /*
    These are Special Predefined Variables. No Need to Create. These Provide Info About
    Blockchain and Transaction Properties

    Variable	        Type	    Description
    msg.sender	        address	    The address of the account that sent the current transaction.
    msg.value 	        uint	    The amount of Ether sent with the current transaction.
    block.coinbase 	    address	    The address of the miner who mined the current block.
    block.difficulty 	uint	    The difficulty of the current block.
    block.gaslimit 	    uint	    The maximum amount of gas that can be used in the current block.
    block.number 	    uint	    The number of the current block.
    block.timestamp 	uint 	    The timestamp of the current block.
    now	                uint	    An alias for block.timestamp.
    tx.origin 	        address     The address of the account that originally created the transaction (i.e., the sender of the first transaction in the call chain).
    tx.gasprice 	    uint	    The gas price (in Wei) of the current transaction.

    */

    address public MyAdress=msg.sender;
    uint public Difficulty=block.difficulty;
    uint public Cost=tx.gasprice;
    uint public Time=block.timestamp;
}
```
---
6. View Pure and Simple

```solidity
contract ViewPureSimple{
    /*
    Functions Are of Three Types 1) View 2) Pure and 3) Simple
    1) View:-   These Are Read Only Blockchain, State Variables and Global Variables. Never Update Them
    2) Pure:-   These Never Read and Update(Write) Blockchain, State Variables and Global Variables
    3) Simple:- They Update the State Variable. No Neeed to Mention Simple Keyword. This Dont
                Return Anything
    */

    uint8 public Age=20;

    function MyView() public view returns (uint) {
        return  Age+10;
    }

    function MyPureOne() public pure returns (uint){
        return  1;
    }
    function MyPureTwo(uint X, uint Y) public pure returns (uint){
        uint Sum=X+Y;
        return  Sum;
    }

    function MySimple() public returns(uint) {
        Age+=23;
        return Age;
    }
}
```
---
7. Default Values

```solidity
contract DefaultValues{
    uint public X;           // 0
    bool public Status;      // false
    address public MyAdress; // 0x0000000000000000000000000000000000000000
    bytes32 public MyBytes;  // 0x0000000000000000000000000000000000000000000000000000000000000000
    string public Name;      // stirng
}
```
---
8. Strings in Solidity

```solidity
contract MyString{
    //State Variables Stored in Blockchain Storage, No Need to Declared Memory Keyword
    string public Name="Muhammad Zubair";

    /*
    Becausse Functins and Local Variables Stored in Memory or Stack , That's Why We
    Using Memory Keyword Inside Functions
    */

    function GetAndSetString(string memory ArgName) pure  public returns(string memory) {
        // string memory Name="Zubair";
        string memory MyName=ArgName;
        return MyName;
    }
}
```
---
9. Constants in Solidity

```solidity
contract MyConstants{

    // The Variable With Constant Keyword Will Cost Low Gas
    address constant public MyAdressA=0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;

    // The Variable Without Constant Keyword Will Cost High Gas
    address public MyAdressB=0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;

}
```
---
10. Constructor in Solidity

```solidity
contract Constructor{
    uint public Age;
    string public Name;
    address public Owner;

    // Constructor is the Functions That is Invoked Fitrst. If Not Defined. Constructor Defined It

    // constructor(){
    //     Age=20;
    //     Name="Zubair";
    //     Owner=msg.sender;
    // }

    constructor(uint _Age, string memory _Name, address _Owner){
        Age=_Age;
        Name=_Name;
        Owner=_Owner;
    }

}
```
---
11. If Else in Solidity

```solidity
contract IfElse{
    /*
    If Else Cannot Defined at Contract Level (Where State Variable Defined)
    They Only Defined At Local Level
    */

    function Check(uint Age) public pure returns(string memory){
        string memory Message;

        if(Age>100){
            Message="Greater Than 100";
        }
        else if(Age<100){
            Message="Less Than 100";
        }
        else{
            Message="Equal 100 or Error";
        }

        return Message;
    }
}
```
---
12. Ternary Operator in Solidity

```solidity
contract Ternary {
    function Check(uint Age) public pure returns(string memory){
        string memory Message;

        Message=Age>100?"Greater Than 100":"Less or Equal to 100";
        return Message;
    }
}
```
---
13. All Types of Loops in Solidity

```solidity
contract MyLoops{

    /*
    Loops Also Don't Work at Contract Level Like Conditional Statement
    You Should Be Carefull While Loops. They Can Cost
    */

    function AllLoops() public pure returns(uint,uint,uint){
        uint For;
        uint While;
        uint DoWhile;

        for (uint I=0; I<10; I++)
        {
            For+=I;
        }

        uint J=0;
        while (J<10)
        {
            While +=J;
            J++;
        }

        uint K=0;
        do{
            DoWhile+=K;
            K++;
        } while(K<10);

        return (For,While,DoWhile);
    }
}
```
---
14. Continue and Break in Solidity

```solidity
contract ContinueAndBreak {
    function MyFunc() public pure returns (uint256) {
        uint256 For;

        for (uint256 I = 0; I < 10; I++) {
            if (I < 8) {
                continue;
            }
            For += I;

            if (I == 8) {
                break;
            }
        }
        return For;
    }
}
```
---
15. Fixed Size Array in Solidity

```solidity
contract Array{
    //Array Just Like Strings Stored on Blockchain Storage

    uint[5] public OuterArray;
    constructor(){
        OuterArray=[1,2,3,4,5];
    }

    //This Function Will Cost Huge Gas
    function GetArray() public view returns (uint[5] memory) {
        return OuterArray;
    }

    function LocalFunc() public pure returns (uint) {
        uint [] memory MyArra=new uint[](5);

        MyArra[2]=23;

        return MyArra[2];
    }

    function Mabipulate() public {
        //Update Array
        OuterArray[2]=23;

        //Delete Element
        delete OuterArray[3];

        //Get Length
        uint Length=OuterArray.length;
    }
}
```
---
16. Dynamic Size Array in Solidity

```solidity
contract DynamicArray {
    /*
    Dynamic Size Arrays Cannot Be Created In Memory. They Have Push and Pop Method. This Can be Initialized in Functio, Constructor
    */
    uint256[] public OuterArray = [1, 2, 3, 4, 5, 6];

    function GetArray() public view returns (uint256[] memory) {
        return OuterArray;
    }

    // See We Cannot Create Dynamic Array in Memory

    // function LocalFunc() public pure{
    //     uint256[] memory MyArra = new uint256[];
    // }

    function Manipulate() public {
        // Update Array
        OuterArray[2] = 23;

        //Delete Element
        delete OuterArray[3];

        //Get Length
        uint256 Length = OuterArray.length;

        // Push Element At Last
        OuterArray.push(100);
        OuterArray.push(200);
        OuterArray.push(300);
        OuterArray.push(400);

        // Pop Element From Last
        OuterArray.pop();
    }
}
```
---
17. Bytes (Fixed Size) in Solidity

```solidity
contract MyFixedBytes{
    /*
    1) Bytes are Similar to Arrays, But They Stored Values in Hexadecimal
    2) bytes#. Here # is any Number. If # is 5 Then It Will Create 5 Boxes
    3) Each Box is of 1 Byte (8 Bit)
    4) Each Box Contains 2 Hexadecimal Digits. So Each Digit 4 Bits
    5) Data Types are of Two Types 1) Value 2) Refrence. Bhtes are Refrence Types
    */

    bytes6 public Name; //Default 0x000000000000
    bytes2 public Age;  //Default 0x0000

    function SetValues() public {
        Name="Zubair";  //Store Like That 0x5a7562616972
        Age="20";       //Store Like That 0x3230
    }
    function GetSize() public view returns (uint,uint){
        return (Name.length, Age.length);
    }
    function GetEach(uint X) public view returns (bytes1,bytes1){
        return (Name[X],Age[X]); //Answer is 6,2
    }
}
```
---
18. Bytes (Dynamic Size) in Solidity

```solidity
contract DynamicBytes{
    bytes public Temp;

    constructor(){
        Temp="Muhamamd Zubair ";
    }
    function Push() public {
        Temp.push('r');
    }
    function Pop() public {
        Temp.pop();
    }
    function Length() view public returns (uint) {
        return Temp.length;
    }
    function GetEach(uint ID) public view returns(bytes1){
        return Temp[ID];
    }
}
```
---
19. Enums in Solidity

```solidity
contract Enums{
    /*
        1) These are User Defined Data Types
        2) Used When We Have More Than 2 Choices Unlike Boolean
        3) Can Be Used For Naming Convention For Integers
        4) Increase Readability. Helps Easy Maintanance of Smart Contract
        5)
    */

    enum Status{
        PENDING,
        REJECTED,
        SHIPPED,
        ACCEPTED,
        CANCEL
    }
    Status MyStatus; //This Have Default Value 0 (PENDING);

    function SetStatus(Status ID /*ID Will Be A Number*/) public {
        MyStatus=ID;
    }
    function SetReject() public {
        MyStatus=Status.REJECTED;
    }
    function ResetStatus() public {
        delete MyStatus; //This Will Again Set MyStatus to 0 (Pending)
    }
    function GetStatus() public view returns(Status) {
        return MyStatus; //O or 1 or Else
    }
}
```
---
20. Struct in Solidity

```solidity
contract MyStruct{
    /*
        1) This is Another User Defined Refrence Type Data
        2) Group of One or More In-Built Data Types
        3) By Default Stored In Storage
        4) Can Be Defined Inside or Outside Contract
        5) If Declared Outside, Will Be Accessed By Multiple Contracts
    */

    struct Employee{
        string Name;
        uint Age;
        address Account;
    }

    Employee public Single;
    Employee[] public Array;

    constructor(uint _Age, string memory _Name, address _Acc){
        Single.Name=_Name;
        Single.Age=_Age;
        Single.Account=_Acc;
    }

    function SetValues() public {
        // Two Ways to Create Instance of IT
        Employee memory E1=Employee("Zubair",20,msg.sender);
        Employee memory E2=Employee({Name:"Talha",Age:20,Account:msg.sender});

        Array.push(E1);
        Array.push(E2);
    }

    function Manipulate() public returns (Employee memory,Employee memory){
        // By Copy
        Single=Array[1];

        delete Array[1];

        // This is Also By Copy. Changes In Temp Wont Reflect in Single
        Employee memory Temp=Single;
        Temp.Name="Kabeer";

        // This is Also By Refrence. Changes In NewTemp Will Reflect in Single
        Employee storage NewTemp=Single;

        // NewTemp.Name="Kabeer Shah";

        return (Temp,NewTemp);
    }
}
```
---
21. Mapping & Advanced Mapping in Solidity

```solidity

/*
    1) Mapping (Key Value Pairs) is also a Data Type
    2) They Connot be Declared at File Level and Function Level
    3) Key Can Be of ENUM,Values, and Contract Types
*/

contract BasicMapiing {
    mapping(uint256 => string) public Employee;

    function SetValues() public {
        Employee[15] = "Zubair";
        Employee[16] = "Talha";
        Employee[17] = "Kamran";
        Employee[18] = "Naheed";
        Employee[19] = "John";
    }

    function GetValues(uint256 ID) public view returns (string memory) {
        return Employee[ID];
    }
}

struct DonorInfo {
    string Name;
    uint256 Age;
    string Addr;
    uint256 Amount;
}

contract AdvanceMapping {
    mapping(address => DonorInfo) public NGO;

    function SetInfo(
        string memory Name,
        uint256 Age,
        string memory Addr,
        uint256 Amount
    ) public {
        NGO[msg.sender] = DonorInfo(Name, Age, Addr, NGO[msg.sender].Amount+Amount);
    }

    function DeleteInfo(address Add) public {
        delete NGO[Add];
    }
}
```
---
22. Visibility in Solidity

```solidity
contract Visibility {
    /*
        1) Visiblity Used By Function and State Variables
        2) Who can Call or Access Function and State Variables
        3) These Are of 4 Types 1) Public 2) Private 3) Internal 4) External
        4) PotentialCaller of 4 Types
            a) Inside Itself Contract
            b) Derived Contract to His Parent Contract (Inheritence)
            c) Another Contract (No Relation Between Contract, But In Same File)
            d) Outside World (Buttons in Remix IDE)

            Gas Order (Low to High) & Security(High to Low) => Private->Internal->External->Public

        5) Private:-    State Variablae (SV) and Function Accessed only Inside Contract
        6) Internal:-   Within Contract and Child Contract
        7) External:-   Only For Function (No SV). Not Allowed to Call for Derived and Contract Itself . Also Call in Outside World (Button in IDE)
        8) Public:- Can Be Called by Any Potential Caller.

        By Defaults SV Are Internal and Functions are Public
    */

    uint256 private X = 1; // Only Within Contract
    uint256 internal Y = 2; // Within Contract and Derived Contarct
    uint256 public Z = 3; // EveryWhere

    function CheckA() public pure returns (string memory) {
        return "Public";
    }

    function CheckB() private pure returns (string memory) {
        return "Private";
    }

    function CheckC() internal pure returns (string memory) {
        return "Internal";
    }

    function CheckD() external pure returns (string memory) {
        return "External";
    }
    function CheckAll() public pure returns (string memory) {
        // return CheckA(); //Works
        // return CheckC(); //Works
        // return  CheckB(); //Works
        // return  CheckD(); //Not Works

    }
}
---
contract Child is Visibility {
    string public ResultA = CheckA(); //It Works Result="Public"
    // string public ResultB = CheckB(); //It Did'nt Works
    string public ResultC = CheckC(); //It Works Result="Internal"
    // string public ResultD = CheckD(); //It Did'nt Works
}
contract TempContract{
    Visibility V1=new Visibility();

    function External() public view returns(string memory) {
        return V1.CheckD(); //Works
        // return V1.CheckA(); // Works
        // return V1.CheckB(); //Not Works
        // return V1.CheckC(); //Not Works

    }
}
```
---
23. Inheritence in Solidity

```solidity
contract Inheritence {
    // Virtual Keyword allows Child to Ovverride Its Implementation

    function A() public pure returns (string memory) {
        return "I am Inside A";
    }

    function B() public pure returns (string memory) {
        return "I am Inside A";
    }

    function C() public pure virtual returns (string memory) {
        return "I am Inside A";
    }

    function D() public pure virtual returns (string memory) {
        return "I am Inside A";
    }
}

contract Child is Inheritence {
    function C() public pure override  returns (string memory) {
        return "I am Inside B";
    }

    function D() public pure virtual  override  returns (string memory) {
        return "I am Inside B";
    }
}
contract GrandChild is Child{
        function D() public pure virtual  override  returns (string memory) {
        return "I am Inside C";
    }
}
```
---
24. Events and Indexing in Blockchain Solidity

```solidity
contract Events {
    /*
        1) In Solidity, events are dispatched signals that smart contracts can fire. When you call events,
        they cause the arguments to be stored in the transaction's log, which is a special data
        structure in the blockchain.

        2) Max Indexing Can be of 3 Variable

        3) Placing the “indexed” keyword in front of a parameter name will store it as a topic in the log record.
        Without the keyword “indexed”, it will be stored as data.
    */

    event Alert(address Account,string Text, uint Balance);

    // If You Want to Keep Indexing Below is The Method
    // event Alert(address indexed Account,string indexed Text, uint indexed Balance, uint Extra);

    function SetEvent(uint Val) public {
        emit Alert(msg.sender, "Has Total Balance Of : ", Val);
    }
}
```
---
25. Multiple Inharitance in Solidity

```solidity
contract MultipleInheritence{
    uint public A;

    constructor(){
        A=100;
    }

    function FunA() public {

    }
}
contract Child is MultipleInheritence {
    uint public B;

    constructor (){
        A=250;
        B=500;
    }
    function FunB() public {

    }
}

/*
    Multiple Inheritence Order Is Frm Less Biased to More Biased.
    It Canntot Be Child,MultipleInheritence. Dues To It Solve the
    Diamond Problem and Cannot Have Duplicate Properties of Its
    Parents. Preference is From Right to Left
*/
contract GrandChild is MultipleInheritence,Child{

}
```
---
26. Overriding in Multiple Inharitance in Solidity

```solidity
contract Overriding{
    uint public A;
    constructor(){
        A=1;
    }
    function Fun() public pure virtual returns(string memory) {
        return "Hello From A";
    }
}
contract Child is Overriding{
    uint public B;
    constructor(){
        B=2;
    }
    function Fun() public pure override virtual returns(string memory) {
        return "Hello From B";
    }
}
contract GrandChild is Overriding,Child{
    uint public C;
    constructor(){
        C=3;
    }

    // Due to Multiple Inheritence We Have to Use override(Child,Overriding). This is Mendatory
    function Fun() public pure override(Child,Overriding) returns(string memory) {
        return "Hello From C";
    }
}
```
---
27. Passing Parameter to Parent Constructor in Multiple Inharitance in Solidity

```solidity
contract A{
    uint public Age;
    string public Name;

    constructor(uint _Age,string memory _Name){
        Age=_Age;
        Name=_Name;
    }
}
contract B{
    uint public Salary;
    string public Adress;

    constructor(uint _Salary,string memory _Adress){
        Salary=_Salary;
        Adress=_Adress;
    }
}

//Following Are Ways to Passing Parameter to Parent Constructor in Multiple Inharitance
contract C is A(20,"Zubair"),B(100,"Lahore"){

}
//Order of Execution is A,B,D
contract D is A,B{
    constructor() A(20,"Zubair") B(100,"Lahore"){

    }
}
//Order of Execution is A,B,E
contract E is A,B{
    constructor(uint _Age,string memory _Name,uint _Salary,string memory _Adress) A(_Age+10,_Name) B(_Salary*5,_Adress) {

    }
}
//Order of Execution is A,B,F
contract F is A(20,"Talha"),B{
    constructor(uint _Salary,string memory _Adress) B(_Salary*2,_Adress) {

    }
}
```
---
28. Calling Parent Function in Multiple Inharitance in Solidity

```solidity
// 1) By Direct Calling
// 2) By Super Method
contract A {
    event Alert(string Message, uint256 Salary);

    function Fun() public virtual {
        emit Alert("A Has Salary : ", 500);
    }
}

contract B is A {
    function Fun() public override  virtual {
        emit Alert("B Has Salary : ", 600);
        A.Fun(); // This is Called Direct Calling

        super.Fun(); //This Can Also Call Parent
    }
}
contract C is A,B {
    function Fun() public override(A,B) {
        emit Alert("C Has Salary : ", 700);

        //This Will Check From Right to Left
        super.Fun(); //This Can Also Call Parent

        // This Will Print
        /*
        C Has Salary : , 700 //By C Contract

        B Has Salary : , 600 //By B Contract
        A Has Salary : , 500 //By B Contract

        A Has Salary : , 500 //By A Contract
        */
    }
}
```
---
29. Require in Solidity

```solidity
contract Require{
    /*
        1) It is Used Fir Error Handling in Function
        2) Used For Input Validation
        3) Also Used For Acess Control
        4) Also Refund Gas if Condition Get False
        5) If Condition Get Fasle, Changes in State Variables By That Function also Reverted
        and Statements After Require Wo'nt Be Executed
    */

    uint public Age=20;
    address Owner;

    constructor(){
        Owner=msg.sender;
    }

    function Check(uint X) public {
        Age+=10;
        require(X>5,"Values is Less < 5");
    }

    function OnlyOwner() public {
        require(Owner==msg.sender,"Not Owner");
        Age-=2;
    }
}
```
---
30. Revert and Assert in Solidity

```solidity
contract RevertAndAssert{
    /*
        1) Work Same as require(), But Condition is Given in IF-ELSE
        2) Undo Also Works Same as require()
        3) We Can Define Custom Error in Revert, Higher Error String Cost Higher Gas

        4) To Check Bug and Security of Contract We Use Assert
        5) If Found Bug Transaction Will Be Stopped
    */

    uint public Age;
    address Owner ;
    constructor(){
        Owner=msg.sender;
    }

    error CustomError(string,address); // Used For Custmom Error Handling

    function Revert(uint Amount) public {
        if(Amount<10){
            // revert("Amount Lesser <10"); //Cost Hight Gas
            Age+=5;
            revert CustomError("Amount Lesser <10",msg.sender); //Cost Low Gass, Custom Error
        }
    }

    function Assert() public {
        assert(Owner==msg.sender);
        Age+=5;
    }
}
```
---
31. Function Modifiers in Solidity

```solidity
contract MyContract {
    /*
        1) Modifier is Special Type of Function
        2) Increase Reusability, Decrease Code Repeating
        3) To Add Function Pre-Requisite
        4) Can Be Multiple Modifiers in a Contract

    */
    uint256 public Age = 0;

    modifier RepeatedCode() {
        for (uint256 I = 0; I < 10; I++) {
            Age += I;
        }

        _; //This Means Go Back to Callee Function to Execute Remaining Code
    }
    modifier Check(uint256 Val) {
        require(Age >= Val, "Less Than 10");
        _;
    }

    function FunA() public RepeatedCode Check(45) {}

    function FunB() public RepeatedCode Check(90) {}

    function FunC() public RepeatedCode Check(135) {}
}
```
---
32. Payable in Solidity 

```solidity
contract MyContract{
    /*
        1) Payable is Ued to Make Adresses Payable
        2) With This You Can Send Ethers to Those Adresses To Whom You Make Payable
        3) If a Function is Payable Then Ethers Will be Added to That Contarct
        In Which Function is Defined
        4) Payable Function Can Be Pure and View Type
        5) If Button Red then Payable, If Yellow Simple, If Blue Then View or Pure of SV;
        6) A Payble function that can receive Ether and respond to an Ether deposit for
        record-keeping purposes
        7) 1Eth=10^18Wei
    */

    // This State Variable is Payable
    address payable public Adress=payable(msg.sender); //To Make Adress Payble ,We Have to Typecast

    // This is How to Make Constructor Payble
    constructor() payable {

    }

    // This Function is Payable
    function ReceiveEther() payable public returns (string memory)  {
        return "Received Amount";
    }

    function CheckBalance() public view returns(uint) {
        return address(this).balance; // Return address(this) Adress of Contract
    }
}
```
---
33. Fallback and Receive in Solidity

```solidity
contract FallbackAndReceive{

    /*
        A) Fallback

        1) It is Executed When Non-Existence Func is Called on Contract
        2) It is Required to Makred External
        3) It Has No Name, No Argument, Not Return Anything
        4) Can Be Defined One Per Contract
        5) If Not Marked Payable, Will Throw Exception If Contarct Receives Ether
        6) Main Usage is to Directly Send ETH to Contarct
        7) Can Receive Data and Ether Both

        B) Receive

        1) It is Executed When Non-Existence Func is Called on Contract
        2) It is Required to Makred External
        3) It Has No Name, No Argument, Not Return Anything
        4) Can Be Defined One Per Contract
        5) If Not Marked Payable, Will Throw Exception If Contarct Receives Ether
        6) Main Usage is to Directly Send ETH to Contarct
        7) Can Receive Ether Only. Not Receive Data From Low Level Interaction
    */

    event Alert(string Text,uint Amount);

    // Use Low Interaction Button For Data Sending and Set Value Section for Sending Amount (Ether)

    /*
    First Deploy Contract and Then Set Value and Then Put Data in Low Level Interaction and
    Click Trasact Button.

    */
    fallback() external payable {
        emit Alert("Fallback) Amount Received Is :", msg.value);
    }

    receive() external payable {
        emit Alert("Receive) Amount Received Is :", msg.value);
    }

    function CheckBalance() public view returns (uint){
        return address(this).balance;
    }

}
```
---
34. Send Ether, Transfer, Call in Solidity

```solidity
contract SendETH{
    /*
        1) Will Se How to Send Ether To Account or Another Contract
        2) Three Method a) Send b) Trafser c) Call

        a) Send:- Used to Trafser Ether to Adress of Account od Contarct. In Result Got Bool Value.
        Has Limit of 2300 Gas. If Gas Cost >2300 Then Transaction Fail and Cost all Gas. Always Use
        Require With It

        b) Transfer:- Gas Limit of 2300. Nothing Get Returned. Changes in State Variable is Reverted.
        No Need to Use Required.

        c) Call:- We Ourself Decide Gas Limit. Get Bool Type Returned Value and Bytes (Having Some Data).
        We Need to Use Require, Because It Dont Revert Changes as Send Function.

        We Generally Use Call and Trafser. Highly Used is Call
    */

    address payable public Receiver=payable (0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2);

    receive() external payable  {

    }
    function CheckBal() public view returns(uint){
        return address(this).balance;
    }

    /*
    For Below 4 Method We ave to First Transact Few Ethers to Our Contarct
    Amount First Will Be Saved in This Contract and Then We Choose to Move From contract
    to Receiver Acouont
    */

    //Using Send Method
    function SendContractToAdress() public {
        bool Ans=Receiver.send(5000);
        require(Ans,"Transaction Failed");

    }
    //Using Transfer Method
    function TransferContractToAdress() public {
        Receiver.transfer(5000);
    }

    //Using Call Method. Default Gas Limit is 3000000
    function CallContractToAdress() public {
        (bool Status,)=Receiver.call{value:500}("");

        require(Status,"Transfer Failed");
    }

    //For Dynamic Adress

    // function CallContractToAdress(address payable Receiver) public {
    //     (bool Status,)=Receiver.call{value:500}("");

    //     require(Status,"Transfer Failed");
    // }

    // ======================================================

    /*
    First Deploy, Then Select Value() Amount Ether and Then Call This Function and Input
    Gette Account Adress

    This is Direct Sending, Amount Move Directly From Function to Getter Account
    */
    function DirectContractToAdress(address payable Getter) payable public {
        (bool Status,)=Getter.call{value:msg.value}("");

        require(Status,"Transfer Failed");
    }

    function DirectContractToContract(address payable Getter) payable public {
        (bool Status,)=Getter.call{value:msg.value}("");

        require(Status,"Transfer Failed");
    }
}

/*
Now This is Illustraction of Sending Amount From Contarct to Contract
First Copies the ADress of Receiver Smart Contarct
*/

contract Sample{

    function CheckBal() public view returns(uint){
        return address(this).balance;
    }

    function DirectContractToContract(address payable Getter) payable public {
        (bool Status,)=Getter.call{value:msg.value}("");

        require(Status,"Transfer Failed");
    }
}
```
---
35. Immutablity in Solidity

```solidity
contract Immutablity{
    /*
        1) Immutable Transcation Cost Is High Than Constant
        2) We Can Change Its Value at Two Places 1) Inline 2) At Deploy Time
        3) Constants Are Initialized at Inline Only
        4) If We Change Immuatable Variable Values in Any Function, It Wont Change

        5) Cost Wise Order (Hight to Low) :- Simple->Immutable->Constant
    */

    address public immutable OwnerA=msg.sender; //400 Gas
    address public immutable OwnerB; //356 Gas. This Give Error, Can Be Resolve By Initializing it in Constructor

    // address public constant C; //This Give Error, Asking to Intialize It Inline
    address public constant OwnerC=address(1); //378 Gas
    address public OwnerD=address(1); //2555 Gas

    constructor(){
        OwnerB=msg.sender;
    }
}
```
---
36. Storage vs Calldata vs Memory in Solidity

```solidity
contract Test {
    /*
        ==Storage==
        1) Storage Holds State Variables
        2) Inside Blockchain
        3) Cost High Gas 
        4) Data is Permanent

        ==Memory==
        1) Memory Hold Local Variable
        2) Data Not Permanent
        3) Inside Mmeory or Stack
        4) Also Cost Gas But Negligible
        5) Function Inputs or Outputs are Also in Memory

        ==Calldata==
        1) Aslo Inside Memory
        2) Cost Low Gas
        3) Data Inside Calldata Can Never Be Changed
        4) Function Input Can Be Passed to Another Function as Input. Dont 
        Create Redundency
    */

    uint256[] public Arr = [1, 2, 3, 4, 5];

    // Data is Copied
    function Storage() public {
        uint256[] storage ARRS = Arr;
        ARRS[1] = 1;
    }

    //Data is Pointing (Refered)
    function Memory() public view {
        uint256[] memory ARRM = Arr;
        ARRM[1] = 1;
    }

    function TempMemory(string memory Name, uint256[] memory TempArr) public {
        /*
            Memory Type Data Can Be Passed to Memory Type Data, But Cannot 
            be Paased to Calldata
        */

        TakeDataA(TempArr); //Works Fine
        // TakeDataB(TempArr); //Will Cause Error
    }

    function CallData(string calldata Name, uint256[] calldata TempArr) public {
        /*
            Calldata Type Data Can Be Passed to Memory as well as Calldata
            This Will Cause Very Low Gas, Because Calldata to Calldata 
            Does Not Create New Instance in Mmeory
        */
        
        TakeDataA(TempArr); // Works Fine
        TakeDataB(TempArr); // Works Fine
    }

    function TakeDataA(uint256[] memory TempArr) public {}

    function TakeDataB(uint256[] calldata TempArr) public {}
}
```
---
37. Inbuilt Cryptographic Hash Function in Solidity

```solidity
contract AllHash{
    /*
        Hashes are 1)SHA256, 2) Rimped160 3) Keccak256

        1) SHA256:- Input Bytes , Output Hash 32 Bytes (Hugly Used)
        1) Ripemd160:- Input Bytes, Ouput 20 Bytes
        1) Keccak256:- Input Bytes , Output Hash 32 Bytes (Hugly Used)

        These are Used in Cotract Signature and Creating ID

        ABI encodes the given arguments. Arguments can be of any type.
        It returns the encoded data as bytes 
        
        ABI encodePACKED the given arguments. Arguments can be of any type.
        It returns the encoded data as bytes . But Different Byytes From ABI Encode
        This Also Compress Bytes
    */

    function KECCAK256(uint X, string memory Name, address Add) pure public returns (bytes32){
        return keccak256(abi.encode(X,Name,Add));
        // return keccak256(abi.encodePacked(X,Name,Add));
    }
    
    function SHA56(uint X, string memory Name, address Add) pure public returns (bytes32){
        return sha256(abi.encode(X,Name,Add));
        // return sha256(abi.encodePacked(X,Name,Add));
    }
    
    function RIPEMD160(uint X, string memory Name, address Add) pure public returns (bytes32){
        return ripemd160(abi.encode(X,Name,Add));
        // return ripemd160(abi.encodePacked(X,Name,Add));

    }
}
```
---
&nbsp;

<a href="https://github.com/HydraPhyzer">![avatar](https://images.weserv.nl/?url=avatars.githubusercontent.com/u/106366894?v=4&h=100&w=100&fit=cover&maxage=7d) &nbsp;&nbsp; </a>

### This is Me The Maker Of This Solidity Cheatsheet. Dont Forget to Give This Repository a Like 💛. &nbsp;


### Feel Free to Start and Clone This Repo. Happy Learning Bye 👋.
