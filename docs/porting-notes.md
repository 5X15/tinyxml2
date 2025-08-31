# Porting Notes

## API Surface
TinyXML-2's public API centers around a set of classes for representing and manipulating XML documents:

- `XMLDocument`
- `XMLElement`
- `XMLAttribute`
- `XMLComment`
- `XMLText`
- `XMLDeclaration`
- `XMLUnknown`
- `XMLPrinter`
- Utility and support types such as `StrPair`, `DynArray`, `MemPool`, `MemPoolT`, `XMLVisitor`, `XMLUtil`, `XMLNode`, `XMLHandle`, and `XMLConstHandle`

Key enumerations include `StrPair::Mode`, `XMLError`, `XMLElement::ElementClosingType`, `Whitespace`, and `XMLPrinter::EscapeAposCharsInAttributes`, along with several internal buffer-size and entity-range enums.

## Memory Model
An `XMLDocument` may be stack-allocated or heap-allocated. Sub-nodes like `XMLElement` and `XMLText` are created through the owning `XMLDocument` and remain owned by it. Deleting the document automatically deletes all child nodes.

## Threading
The library maintains global state for certain settings such as boolean serialization, which is not thread safe. TinyXML-2 performs no internal synchronization; access to a document from multiple threads must be externally synchronized.

