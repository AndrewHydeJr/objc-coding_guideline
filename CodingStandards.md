# GENERAL
----------------------------------------
#### OPERATORS

```objective-c
NSString *foo = @"bar";
NSInteger answer = 42;
answer += 9;
answer++;
answer = 40 + 2;
```

The `++`, `--`, etc are preferred to be after the variable instead of before to be consistent with other operators. Operators separated should **always** be surrounded by spaces unless there is only one operand.

#### ENUMS

```objective-c
typedef enum {
    LSStyleNone = -1,
    LSStyleLight = 0,
    LSStyleDark = 1,
} LSStyle;

```

**Always** have a None enumeration.
**Always** have None be first, and equal to -1.

#### METHODS

All method names should be camel-case, first word lowercase, any other words have the first letter capitalized.

```objective-c
-(void)someMethod 
{
    // Do stuff
}

-(NSString *)stringByReplacingOccurrencesOfString:(NSString *)target withString:(NSString *)replacement 
{
    return nil;
}
```

There should **never** be a space between the `-` or `+` and the return type (`(void)` in this example). 
There should **never** be a space between the return type and the method name.
There should **never** be a space before or after colons. 

If the parameter type is a pointer, there should **always** be a space between the class and the `*`.
The opening bracket should **always** be on the following line.
There should **always** be one new line between methods. 


#### PRAGMA MARK & IMPLEMENTATION

An excerpt of a UIView:

```objective-c
#pragma mark - 
#pragma mark NSOBJECT

- (void)dealloc 
{
    // Release
    [super dealloc];
}

#pragma mark -
#pragma mark UIVIEW

- (id)layoutSubviews 
{
    // Stuff
}

- (void)drawRect:(CGRect)rect 
{
    // Drawing code
}
```

Pragma marks that are not separating the class or superclass methods should conform but are not limited to the following:

```objective-c
#pragma mark ACTIONS
#pragma mark GETTERS
#pragma mark SETTERS
#pragma mark NOTIFICATIONS
#pragma mark UISCROLLVIEW DELEGATE //replace SCROLLVIEW with any delegate
```


# CONTROL STRUCTURES
----------------------------------------
#### IF/ELSE

There should **always** be a space after the control structure (i.e. `if`, `else`, etc).

```objective-c
if (button.enabled) 
{
    // Stuff
} 
else if (otherButton.enabled) 
{
    // Other stuff
} 
else 
{
    // More stuf
}
```

`else` statements should begin on next line as their preceding `if` statement.
    
```objective-c
if (something) 
{
    // Do stuff
}
else 
{
    // Do other stuff
}
```

If there is only one line of code you wish to execute in an `if` or an `else` do **not** use curly braces.

#### SWITCH

```objective-c
switch (something.state) 
{
    case 0: 
    {
        // Something
        break;
    }
    case 1: 
    {
        // Something
        break;
    }
    case 2:
    case 3: 
    {
        // Something
        break;
    }
    default: 
    {
        // Something
        break;
    }
}
```

Brackets are desired around each case. If multiple cases are used, they should be on separate lines. `default` should **always** be the last case and should **always** be included.


#### FOR

Avoid C-style for loops and instead try to stick to Objective-C enumeration of sets. Doing so keeps syntax and conventions along line with Apple's standards.

In order to manipulate an object inside the enumeration, flag the object with <code>__block</code>.

```objective-c
__block NSObject *object = nil;
[someArray enumerateObjectsUsingBlock:^(id obj, NSUInteger idx, BOOL *stop) 
{
    object = obj;
    // do something
}];

[someDictionary enumerateKeysAndObjectsUsingBlock:^(NSString *key, id obj, BOOL *stop) 
{
    // do something
}];
```

If, for some reason, C-style for loops must be used, use the following conventions.

```objective-c
for (NSInteger i = 0; i < 10; i++) 
{
    // Do something
}


for (NSString *key in dictionary) 
{
    // Do something
}
```

When iterating using integers, it is preferred to start at `0` and use `<` rather than starting at `1` and using `<=`. Fast enumeration is generally preferred.

If iterating over an array to look for a specific item, it is preferred to use NSPredicate.

```objective-c
NSArray *array = [currentArray filteredArrayUsingPredicate:[NSPredicate predicateWithFormat:@"name == 'Jim'"]];
```

#### WHILE

```objective-c
while (something < somethingElse) 
{
    // Do something
}
```

### PREFIX

Adding frameworks that are used in the majority of a project to a header prefix is preferred. If these frameworks are in the header prefix, they should **never** be imported in source files in the project. 

When using core data, it is best to import the data model classes into the prefix.

For example, if a header prefix looks like the following:

```objective-c
#ifdef __OBJC__
    #import <Foundation/Foundation.h>
    #import <UIKit/UIKit.h>
#endif
```

## PROPERTIES
------------------------------------

```objective-c
@property (nonatomic, retain) UIColor *topColor;
@property (nonatomic, assign) CGSize shadowOffset;

```

Properties should **only** be used in the .h file when it is necessary for a parent class to set/get the data. 


## PRIVATE METHODS AND PROPERTIES

MyShoeTier.h

```objective-c
@interface MyShoeTier : NSObject

@property (nonatomic, retain) MyShoe *shoe;

@end
```

MyShoeTier.m

```objective-c
#import "MyShoeTier.h"

@interface MyShoeTier ()

@property (nonatomic, retain, readwrite) MyShoe *shoe;
@property (nonatomic, retain) NSMutableArray *laces;

@end

@implementation MyShoeTier

//...

@end
```

#### NAMING

In general, everything should be prefixed with an app specific prefix.

```objective-c
ESPNLoadingView // Simple view that can be used in other applications
SCAppDelegate // Application specific code
```

# MEMORY MANAGEMENT
------------------------------------------

**Always** use Manual Reference Counting

If you alloc, copy, retain, new, you must release.

If you are returning a method you need to release always do it as follows

```objective-c
-(UIView *)createViewWithFrame:(CGRect)frame
{
	UIView *view = [[UIView alloc]initWithFrame:frame];
	
	return [view autorelease];
}
```

# LITERALS
------------------------------------------

We should take full advantage of the literals introduced with iOS 6.

#### DICTIONARIES

```objective-c
NSDictionary *dict = [NSDictionary dictionaryWithObjectsAndKeys:object, @"key", nil];
```

should become:

```objective-c
NSDictionary *dict = @{object:@"key"};
```
#### ARRAYS

```objective-c
NSArray *array = [NSArray arrayWithObjects:@"one", @"two", nil];
```

should become 

```objective-c
NSArray *array = @[@"one", @"two"];
```
#### NSNUMBERS

```objective-c
NSNumber *number = [NSNumber numberWithInt:0];
```

should become

```objective-c
NSNumber *number = @0;
```

# DESIGN PATTERNS
-----------------------------------
## DELEGATES

## BLOCKS

# SETTERS


