# DataInput und DataOutput

...Interfaces des java.io Packages, welche Methoden zur Ein- und Ausgabe elementarer Datentypen sowie Zeichenketten einheitlich definieren.

- DataInput -> Ausgabe elementarer Datentypen/ Zeichenketten in Programm
- DataOutput -> Eingabe elementarer Datentypen/ Zeichenketten aus Programm

## Methoden

...verschiedene Methoden zum Lesen/Schreiben verschiedener Datentypen.

| Datentyp | DataInput             | DataOutput                   |
|----------|-----------------------|------------------------------|
| Boolean  | boolean readBoolean() | void writeBoolean(boolean b) |
| Char     | char readChar()       | void writeChar()             |
| Byte     | byte readByte()       | void writeByte(int b)        |
|          |                       | void write(int b)            |
| Short    | short readShort()     | void writeShort(int s)       |
| Integer  | int readInt()         | void writeInt(int i)         |
| Long     | long readLong()       | void writeLong(long l)       |
| Float    | float readFloat()     | void writeFloat(float f)     |
| Double   | double readDouble()   | void writeDouble(double d)   |
| String   | String readUTF()      | void writeUTF(String s)      |
| String   | String readLine()     | void writeChars(String s)    |
|          |                       | void writeBytes(String s)    |

## Weitere Methoden

| DataInput                                  | DataOutput                             |
|--------------------------------------------|----------------------------------------|
| void readFully(byte[] b)                   | void write(byte[] b)                   |
| void readFully(byte[] b, int off, int len) | void write(byte[] b, int off, int len) |
| int readUnsignedByte()                     |                                        |
| int readUnsignedShort()                    |                                        |
| int skip(int n)                            |                                        |
