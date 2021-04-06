[TOC]



# Representations of Inserted, Deleted and Moved Statements

There are representations of 22 syntactic types of statements.

In SCMiner, each statement is represented by a vector with various dimensions. The following parts of this file is used to decribe the details of these representations.

Among these representations, there are 3 common features: Type, OP, Parent

## 1. Syntactic Types

The following table lists all the AST node types involved in SCMiner. The column **Encode** list all their corresponding encodes.

| Syntactic Types | Encode |
| ------------------------------------------ | ---- |
|[PACKAGE_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FPackageDeclaration.html)|100|
|[DIMENSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FDimension.html)|200|
|[METHOD_REF_PARAMETER](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FMethodRefParameter.html)|300|
|[COMPILATION_UNIT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FCompilationUnit.html)|400|
|[MODIFIER](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FModifier.html)|500|
|[MEMBER_VALUE_PAIR](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FMemberValuePair.html)|600|
|[INITIALIZER](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FInitializer.html)|7010|
|[ENUM_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FEnumDeclaration.html)|7021|
|[TYPE_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FTypeDeclaration.html)|7022|
|[ANNOTATION_TYPE_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FAnnotationTypeDeclaration.html)|7023|
|[FIELD_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FFieldDeclaration.html)|7030|
|[ANNOTATION_TYPE_MEMBER_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FAnnotationTypeMemberDeclaration.html)|7040|
|[ENUM_CONSTANT_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FEnumConstantDeclaration.html)|7050|
|[METHOD_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FMethodDeclaration.html)|7060|
|[SINGLE_VARIABLE_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSingleVariableDeclaration.html)|8010|
|[VARIABLE_DECLARATION_FRAGMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FVariableDeclarationFragment.html)|8020|
|[NAME_QUALIFIED_TYPE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FNameQualifiedType.html)|9011|
|[QUALIFIED_TYPE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FQualifiedType.html)|9012|
|[PRIMITIVE_TYPE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FPrimitiveType.html)|9013|
|[WILDCARD_TYPE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FWildcardType.html)|9014|
|[SIMPLE_TYPE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSimpleType.html)|9015|
|[UNION_TYPE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FUnionType.html)|9020|
|[INTERSECTION_TYPE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FIntersectionType.html)|9030|
|[ARRAY_TYPE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FArrayType.html)|9040|
|[PARAMETERIZED_TYPE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FParameterizedType.html)|9050|
|[ANONYMOUS_CLASS_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FAnonymousClassDeclaration.html)|10000|
|[CONSTRUCTOR_INVOCATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FConstructorInvocation.html)|11010|
|[CONTINUE_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FContinueStatement.html)|11020|
|[EXPRESSION_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FExpressionStatement.html)|11030|
|[LABELED_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FLabeledStatement.html)|11040|
|[BLOCK](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FBlock.html)|11050|
|[FOR_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FForStatement.html)|11060|
|[SYNCHRONIZED_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSynchronizedStatement.html)|11070|
|[TRY_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FTryStatement.html)|11080|
|[DO_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FDoStatement.html)|11090|
|[ASSERT_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FAssertStatement.html)|11100|
|[SWITCH_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSwitchStatement.html)|11110|
|[THROW_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FThrowStatement.html)|11120|
|[IF_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FIfStatement.html)|11130|
|[TYPE_DECLARATION_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FTypeDeclarationStatement.html)|11140|
|[ENHANCED_FOR_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FEnhancedForStatement.html)|11150|
|[WHILE_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FWhileStatement.html)|11160|
|[EMPTY_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FEmptyStatement.html)|11170|
|[RETURN_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FReturnStatement.html)|11180|
|[SWITCH_CASE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSwitchCase.html)|11190|
|[VARIABLE_DECLARATION_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FVariableDeclarationStatement.html)|11200|
|[SUPER_CONSTRUCTOR_INVOCATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSuperConstructorInvocation.html)|11210|
|[BREAK_STATEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FBreakStatement.html)|11220|
|[TAG_ELEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FTagElement.html)|12000|
|[FIELD_ACCESS](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FFieldAccess.html)|13010|
|[POSTFIX_EXPRESSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FPostfixExpression.html)|13020|
|[CHARACTER_LITERAL](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FCharacterLiteral.html)|13030|
|[BOOLEAN_LITERAL](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FBooleanLiteral.html)|13040|
|[CONDITIONAL_EXPRESSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FConditionalExpression.html)|13050|
|[INSTANCEOF_EXPRESSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FInstanceofExpression.html)|13060|
|[ARRAY_INITIALIZER](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FArrayInitializer.html)|13070|
|[CREATION_REFERENCE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FCreationReference.html)|13081|
|[TYPE_METHOD_REFERENCE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FTypeMethodReference.html)|13082|
|[SUPER_METHOD_REFERENCE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSuperMethodReference.html)|13083|
|[EXPRESSION_METHOD_REFERENCE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FExpressionMethodReference.html)|13084|
|[THIS_EXPRESSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FThisExpression.html)|13090|
|[ASSIGNMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FAssignment.html)|13100|
|[SUPER_FIELD_ACCESS](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSuperFieldAccess.html)|13110|
|[ARRAY_CREATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FArrayCreation.html)|13120|
|[MARKER_ANNOTATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FMarkerAnnotation.html)|13131|
|[NORMAL_ANNOTATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FNormalAnnotation.html)|13132|
|[SINGLE_MEMBER_ANNOTATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSingleMemberAnnotation.html)|13133|
|[TYPE_LITERAL](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FTypeLiteral.html)|13140|
|[METHOD_INVOCATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FMethodInvocation.html)|13150|
|[QUALIFIED_NAME](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FQualifiedName.html)|13161|
|[SIMPLE_NAME](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSimpleName.html)|13162|
|[NUMBER_LITERAL](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FNumberLiteral.html)|13170|
|[PARENTHESIZED_EXPRESSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FParenthesizedExpression.html)|13180|
|[STRING_LITERAL](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FStringLiteral.html)|13190|
|[INFIX_EXPRESSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FInfixExpression.html)|13200|
|[NULL_LITERAL](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FNullLiteral.html)|13210|
|[SUPER_METHOD_INVOCATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FSuperMethodInvocation.html)|13220|
|[CAST_EXPRESSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FCastExpression.html)|13230|
|[VARIABLE_DECLARATION_EXPRESSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FVariableDeclarationExpression.html)|13240|
|[ARRAY_ACCESS](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FArrayAccess.html)|13250|
|[CLASS_INSTANCE_CREATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FClassInstanceCreation.html)|13260|
|[LAMBDA_EXPRESSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FLambdaExpression.html)|13270|
|[PREFIX_EXPRESSION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FPrefixExpression.html)|13280|
|[IMPORT_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FImportDeclaration.html)|14000|
|[MEMBER_REF](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FMemberRef.html)|15000|
|[OPENS_DIRECTIVE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FOpensDirective.html)|16011|
|[EXPORTS_DIRECTIVE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FExportsDirective.html)|16012|
|[USES_DIRECTIVE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FUsesDirective.html)|16020|
|[PROVIDES_DIRECTIVE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FProvidesDirective.html)|16030|
|[REQUIRES_DIRECTIVE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FRequiresDirective.html)|16040|
|[MODULE_MODIFIER](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FModuleModifier.html)|16050|
|[METHOD_REF](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FMethodRef.html)|16060|
|[TEXT_ELEMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FTextElement.html)|16070|
|[LINE_COMMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FLineComment.html)|17010|
|[JAVADOC](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FJavadoc.html)|17020|
|[BLOCK_COMMENT](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FBlockComment.html)|17030|
|[CATCH_CLAUSE](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FCatchClause.html)|18000|
|[MODULE_DECLARATION](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FModuleDeclaration.html)|19000|
|[TYPE_PARAMETER](https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FTypeParameter.html)|20000|



## 2. Representations templates for 22 syntactic types of statements.




### 1. AssertStatement

 - **Grammar**: <a url=" <https://help.eclipse.org/2019-12/index.jsp?topic=%2Forg.eclipse.jdt.doc.isv%2Freference%2Fapi%2Forg%2Feclipse%2Fjdt%2Fcore%2Fdom%2FAssertStatement.html">assert Expression [ : Expression ]</a>

- **Template**: [Type, OP, Parent, AssertLiteral]

   | Feature       | Description                                                  |
   | :------------ | ------------------------------------------------------------ |
   | Type          | The syntactic type of this statement, i.e., ASSERT_STATEMENT. |
   | OP            | The edit operation, Insert, Delete or Move.                  |
   | Parent        | The syntactic type of the parent node of this statement.     |
   | AssertLiteral | The literal of assert expression.                            |

- **Example**: 

  - code change

  ```
  + assert(m.size() == 1);
  ```

  - Representation result: 

  ```[11100,2,7060,1694803022]```

| Feacture      | Example            | Encode     |
| :------------ | ------------------ | ---------- |
| Type          | ASSERT_STATEMENT   | 11100      |
| OP            | Insert             | 2          |
| Parent        | METHOD_DECLARATION | 7060       |
| AssertLiteral | m.size()==1        | 1694803022 |

### 2. Assignment

- **Grammar**

  ```
  Expression AssignmentOperator Expression
  ```

- **Template**: [Type, OP, Parent, Operator, VariableName, Initializer]

  | Feature      | Description                                              |
  | :----------- | -------------------------------------------------------- |
  | Type         | The syntactic type of this statement, i.e., ASSIGNMENT.  |
  | OP           | The edit operation, Insert, Delete or Move.              |
  | Parent       | The syntactic type of the parent node of this statement. |
  | Operator     | The assignment operator of this statement, e.g, '+'.     |
  | VariableName | The left hand side of this statement.                    |
  | Initializer  | The right hand side of this statement.                   |

- **Example**: 

  - code change

  ```
  + level = new Level();
  ```

  - Representation result: 

  ```[13100,2,7060,43,102865796,664512965]```

| Feacture     | Example            | Encode    |
| :----------- | ------------------ | --------- |
| Type         | ASSIGNMENT         | 13100     |
| OP           | Insert             | 2         |
| Parent       | METHOD_DECLARATION | 7060      |
| Operator     | '+'                | 43        |
| VariableName | ”level“            | 102865796 |
| Initializer  | ”newLevel()“       | 664512965 |

### 3. BreakStatement 

- **Grammar**: 

  ```
  break [ Identifier ] ;
  ```

- **Template**: [Type, OP, Parent, LabelLiteral]

  | Feature      | Description                                                  |
  | ------------ | ------------------------------------------------------------ |
  | Type         | The syntactic type of this statement, i.e., BREAK_STATEMENT. |
  | OP           | The edit operation, Insert, Delete or Move.                  |
  | Parent       | The syntactic type of the parent node of this statement.     |
  | LabelLiteral | The literal of the identifier of this statement.             |

  

- **Example**

  - code change

    ``````
    + break;
    ``````

  - Representation result

  ``````
  [11220, 2, 7060, 0]
  ``````

  | Feacture     | Example            | Encode |
  | ------------ | ------------------ | ------ |
  | Type         | BREAK_STATEMENT    | 11220  |
  | OP           | Insert             | 2      |
  | Parent       | METHOD_DECLARATION | 7060   |
  | LabelLiteral | ""                 | 0      |

### 4. CatchClause 

- **Grammar**: 

  ```
  catch ( FormalParameter ) Block
  ```

- **Template**: [Type, OP, Parent, ExceptionType]

  | Feature       | Description                                               |
  | ------------- | --------------------------------------------------------- |
  | Type          | The syntactic type of this statement, i.e., CATCH_CLAUSE. |
  | OP            | The edit operation, Insert, Delete or Move.               |
  | Parent        | The syntactic type of the parent node of this statement.  |
  | ExceptionType | The class type of the exception variable.                 |

- **Example**

  - code change

    ```
      ...
    + catch (IOException e) {
          ... // Block   
    + } 
    ```

  - Representation result

  ```
  [18000, 2, 7060, -1482501687]
  ```

  | Feacture      | Example            | Encode      |
  | ------------- | ------------------ | ----------- |
  | Type          | CATCH_CLAUSE       | 18000       |
  | OP            | Insert             | 2           |
  | Parent        | METHOD_DECLARATION | 7060        |
  | ExceptionType | “IOException”      | -1482501687 |

### 5. ContinueStatement 

- **Grammar**: 

  ```
  continue [ Identifier ] ;
  ```

- **Template**: [Type, OP, Parent, AssertLiteral]

  | Feature | Description                                                  |
  | ------- | ------------------------------------------------------------ |
  | Type    | The syntactic type of this statement, i.e., CONTINUE_STATEMENT. |
  | OP      | The edit operation, Insert, Delete or Move.                  |
  | Parent  | The syntactic type of the parent node of this statement.     |

- **Example**

  - code change

    ```
    + continue;
    ```

  - Representation result

  ```
  [11]
  ```

  | Feacture | Example            | Encode |
  | -------- | ------------------ | ------ |
  | Type     | CONTINUE_STATEMENT | 11020  |
  | OP       | Insert             | 2      |
  | Parent   | METHOD_DECLARATION | 7060   |

### 6. DoStatement 

- **Grammar**: 

  ```
  do Statement while ( Expression ) ;
  ```

- **Template**: [Type, OP, Parent, Condition]  

  | Feature   | Description                                               |
  | --------- | --------------------------------------------------------- |
  | Type      | The syntactic type of this statement, i.e., DO_STATEMENT. |
  | OP        | The edit operation, Insert, Delete or Move.               |
  | Parent    | The syntactic type of the parent node of this statement.  |
  | Condition | The literal of condition expression of this statement     |

- **Example**

  - code change

    ```
    + do {
         ... // Block
    + } while(condition);
    ```

  - Representation result

  ```
  [11090, 2, 7060, -861311717]
  ```

  | Feacture  | Example            | Encode     |
  | --------- | ------------------ | ---------- |
  | Type      | DO_STATEMENT       | 11090      |
  | OP        | Insert             | 2          |
  | Parent    | METHOD_DECLARATION | 7060       |
  | Condition | "condition"        | -861311717 |

### 7. EnhacedForStatement

- **Grammar**: 

  ```
  for ( FormalParameter : Expression )
                          Statement
  ```

- **Template**: [Type, OP, Parent, ClassName, Initializer] 

  | Feature     | Description                                                  |
  | ----------- | ------------------------------------------------------------ |
  | Type        | The syntactic type of this statement, i.e., ENHACED_FOR_STATEMENT. |
  | OP          | The edit operation, Insert, Delete or Move.                  |
  | Parent      | The syntactic type of the parent node of this statement.     |
  | ClassName   | The class type of the formal parameter of this statement.    |
  | Initializer | The literal of the expression of this satement.              |

- **Example**

  - code change

    ```
    + for (Item item: items.iterator())
          ...
    ```

  - Representation result

  ```
  [11150, 2, 7060, 2289459, -1274312483]
  ```

  | Feacture    | Example               | Encode      |
  | ----------- | --------------------- | ----------- |
  | Type        | ENHACED_FOR_STATEMENT | 11150       |
  | OP          | Insert                | 2           |
  | Parent      | METHOD_DECLARATION    | 7060        |
  | ClassName   | "Item"                | 2289459     |
  | Initializer | "items.iterator()"    | -1274312483 |

### 8. ForStatement

- **Grammar**: 

  ```
  for (
  	[ ForInit ];
  	[ Expression ] ;
  	[ ForUpdate ] )
  	Statement
  ```

- **Template**: [Type, OP, Parent, Condition] 

  | Feature   | Description                                                |
  | --------- | ---------------------------------------------------------- |
  | Type      | The syntactic type of this statement, i.e., FOR_STATEMENT. |
  | OP        | The edit operation, Insert, Delete or Move.                |
  | Parent    | The syntactic type of the parent node of this statement.   |
  | Condition | The literal of the condition expression of this statement. |

- **Example**

  - code change

    ```
    + for (int index = 0; index < size; index ++) {
      ...   
    + }
    ```

  - Representation result

  ```
  [11060, 2, 7060, 714796203]
  ```

  | Feacture  | Example            | Encode    |
  | --------- | ------------------ | --------- |
  | Type      | FOR_STATEMENT      | 11060     |
  | OP        | Insert             | 2         |
  | Parent    | METHOD_DECLARATION | 7060      |
  | Condition | "index<size"       | 714796203 |

### 9. IfStatement

- **Grammar**: 

  ```
  if ( Expression ) Statement [ else Statement]
  ```

- **Template**: [Type, OP, Parent, AssertLiteral]

  | Feature   | Description                                                |
  | --------- | ---------------------------------------------------------- |
  | Type      | The syntactic type of this statement, i.e., IF_STATEMENT.  |
  | OP        | The edit operation, Insert, Delete or Move.                |
  | Parent    | The syntactic type of the parent node of this statement.   |
  | Condition | The literal of the condition expression of this statement. |

- **Example**

  - code change

    ```
    + if (condition) {
         ...
    + }
    ```

  - Representation result

  ```
  [11130, 2, 7060, -861311717]
  ```

  | Feacture  | Example            | Encode     |
  | --------- | ------------------ | ---------- |
  | Type      | IF_STATEMENT       | 11130      |
  | OP        | Insert             | 2          |
  | Parent    | METHOD_DECLARATION | 7060       |
  | Condition | "condition"        | -861311717 |

###  10.LabelStatement 

- **Grammar**: 

  ```
  Identifier : Statement
  ```

- **Template**: [Type, OP, Parent, LabelLitera]

  | Feature     | Description                                                  |
  | ----------- | ------------------------------------------------------------ |
  | Type        | The syntactic type of this statement, i.e., LABELED_STATEMENT. |
  | OP          | The edit operation, Insert, Delete or Move.                  |
  | Parent      | The syntactic type of the parent node of this statement.     |
  | LabelLitera | The literal of label of this statement                       |

- **Example**

  - code change

    ```
    + label: 
      ...
    ```

  - Representation result

  ```
  [11040, 2, 7060, 102727412]
  ```

  | Feacture    | Example            | Encode    |
  | ----------- | ------------------ | --------- |
  | Type        | LABELED_STATEMENT  | 11040     |
  | OP          | Insert             | 2         |
  | Parent      | METHOD_DECLARATION | 7060      |
  | LabelLitera | "label"            | 102727412 |

### 11. MethodInvocation

- **Grammar**: 

  ```
  [ Expression . ]
           [ < Type { , Type } > ]
           Identifier ( [ Expression { , Expression } ] )
  ```

- **Template**: [Type, OP, Parent, MethodName]

  | Feature    | Description                                                  |
  | ---------- | ------------------------------------------------------------ |
  | Type       | The syntactic type of this statement, i.e., METHOD_INVOCATION. |
  | OP         | The edit operation, Insert, Delete or Move.                  |
  | Parent     | The syntactic type of the parent node of this statement.     |
  | MethodName | The name of the invoked method.                              |

- **Example**

  - code change

    ```
    + id.getValue();
    ```

  - Representation result

  ```
  [13150, 2, 7060, 1967798203]
  ```

  | Feacture   | Example            | Encode     |
  | ---------- | ------------------ | ---------- |
  | Type       | METHOD_INVOCATION  | 13150      |
  | OP         | Insert             | 2          |
  | Parent     | METHOD_DECLARATION | 7060       |
  | MethodName | "getValue"         | 1967798203 |

### 12. NewClassInstance

- **Grammar**: 

  ```
  [ Expression . ]
  	new [ < Type { , Type } > ]
  	Type ( [ Expression { , Expression } ] )
  	[ AnonymousClassDeclaration ]
  ```

- **Template**: [Type, OP, Parent, ClassName]

  | Feature   | Description                                                  |
  | --------- | ------------------------------------------------------------ |
  | Type      | The syntactic type of this statement, i.e.,  CLASS_INSTANCE_CREATION . |
  | OP        | The edit operation, Insert, Delete or Move.                  |
  | Parent    | The syntactic type of the parent node of this statement.     |
  | ClassName | The class type of this class instance creation expression.   |

- **Example**

  - code change

    ```
    + new Initializer();
    ```

  - Representation result

  ```
  [13260, 2, 7060, -1393078590]
  ```

  | Feacture  | Example                 | Encode      |
  | --------- | ----------------------- | ----------- |
  | Type      | CLASS_INSTANCE_CREATION | 13260       |
  | OP        | Insert                  | 2           |
  | Parent    | METHOD_DECLARATION      | 7060        |
  | ClassName | "Initializer"           | -1393078590 |

###  13. ReturnStatement

- **Grammar**: 

  ```
  return [ Expression ] ;
  ```

- **Template**: [Type, OP, Parent, ClassName, Expression]

  | Feature    | Description                                                  |
  | ---------- | ------------------------------------------------------------ |
  | Type       | The syntactic type of this statement, i.e., RETURN_STATEMENT. |
  | OP         | The edit operation, Insert, Delete or Move.                  |
  | Parent     | The syntactic type of the parent node of this statement.     |
  | ClassName  | The class type of the returned value.                        |
  | Expression | The literal of the expression of this statement.             |

- **Example**

  - code change

    ```
    + return 1;
    ```

  - Representation result

  ```
  [11180, 2, 7060, -672261858, 49]
  ```

  | Feacture   | Example            | Encode     |
  | ---------- | ------------------ | ---------- |
  | Type       | RETURN_STATEMENT   | 11180      |
  | OP         | Insert             | 2          |
  | Parent     | METHOD_DECLARATION | 7060       |
  | ClassName  | "Integer"          | -672261858 |
  | Expression | "1"                | 49         |

### 14. SwithCase

- **Grammar**: 

  ```
  case Expression  :
       default :
  ```

- **Template**: [Type, OP, Parent, LabelLiteral]

  | Feature      | Description                                                |
  | ------------ | ---------------------------------------------------------- |
  | Type         | The syntactic type of this statement, i.e.,  SWITCH_CASE . |
  | OP           | The edit operation, Insert, Delete or Move.                |
  | Parent       | The syntactic type of the parent node of this statement.   |
  | LabelLiteral | The literal of the expression of this statement.           |

- **Example**

  - code change

    ```
    + case CASE:
      ...
    ```

  - Representation result

  ```
  [11190, 2, 7060, 2061104]
  ```

  | Feacture     | Example          | Encode  |
  | ------------ | ---------------- | ------- |
  | Type         | SWITCH_CASE      | 11190   |
  | OP           | Insert           | 2       |
  | Parent       | SWITCH_STATEMENT | 11110   |
  | LabelLiteral | "CASE"           | 2061104 |

###  15. SwithStatement

- **Grammar**: 

  ```
  switch ( Expression )
  	{ { SwitchCase | Statement } }
  ```

- **Template**: [Type, OP, Parent, Expression]

  | Feature    | Description                                                  |
  | ---------- | ------------------------------------------------------------ |
  | Type       | The syntactic type of this statement, i.e., SWITCH_STATEMENT. |
  | OP         | The edit operation, Insert, Delete or Move.                  |
  | Parent     | The syntactic type of the parent node of this statement.     |
  | Expression | The literal of the expression of this statement.             |

- **Example**

  - code change

    ```
    + switch (cases) {
          ...   
    +}
    ```

  - Representation result

  ```
  [11110, 2, 7060, 94432067]
  ```

  | Feacture   | Example            | Encode   |
  | ---------- | ------------------ | -------- |
  | Type       | SWITCH_STATEMENT   | 11110    |
  | OP         | Insert             | 2        |
  | Parent     | METHOD_DECLARATION | 7060     |
  | Expression | "cases"            | 94432067 |

###  16. SynchronizeStatement

- **Grammar**: 

  ```
   synchronized ( Expression ) Block
  ```

- **Template**: [Type, OP, Parent, AssertLiteral]

  | Feature | Description                                                  |
  | ------- | ------------------------------------------------------------ |
  | Type    | The syntactic type of this statement, i.e.,  SYNCHRONIZED_STATEMENT . |
  | OP      | The edit operation, Insert, Delete or Move.                  |
  | Parent  | The syntactic type of the parent node of this statement.     |
  | Lock    | The literal of the expression of this statement.             |

- **Example**

  - code change

    ```
    + synchronized (lock) {
         ...
    + }
    ```

  - Representation result

  ```
  [11070, 2, 7060, 3327275]
  ```

  | Feacture | Example                | Encode  |
  | -------- | ---------------------- | ------- |
  | Type     | SYNCHRONIZED_STATEMENT | 11070   |
  | OP       | Insert                 | 2       |
  | Parent   | METHOD_DECLARATION     | 7060    |
  | Lock     | "lock"                 | 3327275 |

###  17. ThrowStatement

- **Grammar**: 

  ```
  throw Expression ;
  ```

- **Template**: [Type, OP, Parent, ExceptionType]

  | Feature       | Description                                                  |
  | ------------- | ------------------------------------------------------------ |
  | Type          | The syntactic type of this statement, i.e.,  THROW_STATEMENT . |
  | OP            | The edit operation, Insert, Delete or Move.                  |
  | Parent        | The syntactic type of the parent node of this statement.     |
  | ExceptionType | The class type of the throwed exception.                     |

- **Example**

  - code change

    ```
    + throw new IOException();
    ```

  - Representation result

  ```
  [11120, 2, 7060, -1482501687]
  ```

  | Feacture      | Example            | Encode      |
  | ------------- | ------------------ | ----------- |
  | Type          | THROW_STATEMENT    | 11120       |
  | OP            | Insert             | 2           |
  | Parent        | METHOD_DECLARATION | 7060        |
  | ExceptionType | "IOException"      | -1482501687 |

###  18. TryStatement

- **Grammar**: 

  ```
  try [ ( Resources ) ]
      Block
      [ { CatchClause } ]
      [ finally Block ]
  ```

- **Template**: [Type, OP, Parent, AssertLiteral]

  | Feature | Description                                                 |
  | ------- | ----------------------------------------------------------- |
  | Type    | The syntactic type of this statement, i.e., TRY_STATEMENT . |
  | OP      | The edit operation, Insert, Delete or Move.                 |
  | Parent  | The syntactic type of the parent node of this statement.    |

- **Example**

  - code change

    ```
    + try {
         ... 
    + }
      ...
    ```

  - Representation result

  ```
  [11080, 2, 7060]
  ```

  | Feacture | Example            | Encode |
  | -------- | ------------------ | ------ |
  | Type     | TRY_STATEMENT      | 11080  |
  | OP       | Insert             | 2      |
  | Parent   | METHOD_DECLARATION | 7060   |

###  19. PrefixExpression

- **Grammar**: 

  ```
  PrefixOperator Expression
  ```

- **Template**: [Type, OP, Parent, Operator, VariableName]

  | Feature      | Description                                                  |
  | ------------ | ------------------------------------------------------------ |
  | Type         | The syntactic type of this statement, i.e.,  PREFIX_EXPRESSION . |
  | OP           | The edit operation, Insert, Delete or Move.                  |
  | Parent       | The syntactic type of the parent node of this statement.     |
  | Operator     | The literal of the operator.                                 |
  | VariableName | The literal of the expression.                               |

- **Example**

  - code change

    ```
    + --count;
    ```

  - Representation result

  ```
  [13280, 2, 7060, 1440, 94851343]
  ```

  | Feacture     | Example            | Encode   |
  | ------------ | ------------------ | -------- |
  | Type         | PREFIX_EXPRESSION  | 13280    |
  | OP           | Insert             | 2        |
  | Parent       | METHOD_DECLARATION | 7060     |
  | Operator     | "--"               | 1440     |
  | VariableName | "count"            | 94851343 |

###  20. PostfixExpression 

- **Grammar**: 

  ```
  Expression PostfixOperator
  ```

- **Template**: [Type, OP, Parent, Operator, VariableName]

  | Feature      | Description                                                  |
  | ------------ | ------------------------------------------------------------ |
  | Type         | The syntactic type of this statement, i.e., POSTFIX_EXPRESSION. |
  | OP           | The edit operation, Insert, Delete or Move.                  |
  | Parent       | The syntactic type of the parent node of this statement.     |
  | Operator     | The literal of the operator.                                 |
  | VariableName | The literal of the expression.                               |

- **Example**

  - code change

    ```
    + count--;
    ```

  - Representation result

  ```
  [13020, 2, 7060, 1440, 94851343]
  ```

  | Feacture     | Example            | Encode   |
  | ------------ | ------------------ | -------- |
  | Type         | POSTFIX_EXPRESSION | 13020    |
  | OP           | Insert             | 2        |
  | Parent       | METHOD_DECLARATION | 7060     |
  | Operator     | "--"               | 1440     |
  | VariableName | "count"            | 94851343 |

###  21. VariableDeclaration

- **Grammar**: 

  ```
  { ExtendedModifier } Type VariableDeclarationFragment
          { , VariableDeclarationFragment } ;
  ```

- **Template**: [Type, OP, Parent, ClassName, VariableName, Initialize]

  | Feature      | Description                                                  |
  | ------------ | ------------------------------------------------------------ |
  | Type         | The syntactic type of this statement, i.e.,   VARIABLE_DECLARATION_STATEMENT  . |
  | OP           | The edit operation, Insert, Delete or Move.                  |
  | Parent       | The syntactic type of the parent node of this statement.     |
  | ClassName    | The class type of the declared type.                         |
  | VariableName | The name of the declared variable.                           |
  | Initializer  | The literal of the initialized expression.                   |

- **Example**

  - code change

    ```
    + String str = "SCMiner";
    ```

  - Representation result

  ```
  [11200, 2, 7060, -1808118735, 83473, -1061543403
  ```

  | Feacture     | Example                        | Encode      |
  | ------------ | ------------------------------ | ----------- |
  | Type         | VARIABLE_DECLARATION_STATEMENT | 11200       |
  | OP           | Insert                         | 2           |
  | Parent       | METHOD_DECLARATION             | 7060        |
  | ClassName    | "String"                       | -1808118735 |
  | VariableName | "Str"                          | 83473       |
  | Initializer  | ""SCMiner""                    | -1061543403 |

###  22. WhileStatement 

- **Grammar**: 

  ```
  while ( Expression ) Statement
  ```

- **Template**: [Type, OP, Parent, Condition]

  | Feature   | Description                                                  |
  | --------- | ------------------------------------------------------------ |
  | Type      | The syntactic type of this statement, i.e.,  WHILE_STATEMENT . |
  | OP        | The edit operation, Insert, Delete or Move.                  |
  | Parent    | The syntactic type of the parent node of this statement.     |
  | Condition | The literal of the experssion of this statement.             |

- **Example**

  - code change

    ```
    + while (condition) {
          ...
    + }
    ```

  - Representation result

  ```
  [11160, 2, 7060, -863330171]
  ```

  | Feacture  | Example            | Encode     |
  | --------- | ------------------ | ---------- |
  | Type      | WHILE_STATEMENT    | 11160      |
  | OP        | Insert             | 2          |
  | Parent    | METHOD_DECLARATION | 7060       |
  | Condition | "condition"        | -863330171 |

  
