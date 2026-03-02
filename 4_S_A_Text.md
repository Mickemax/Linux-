# Processing Text Files
    # Filtering Text
       # cut OPTION [FILE]
         - it helps extract small data sections.
                + Text File Records: These are single file line that ends in a newline linefeed.
                 - cat -E : Display every newline feed as $.
                 - cut -z : If your text file records ends in the ASCII character NUL(\0).
                + Text File Records Delimiter: For some options to be used, fields must exist with each within each text file record. these are data that is separated by some delimeter.
                + Text File  Changes: Does not modifies file.
        
        # Basic Regular Expressions ( BRE)
            - It is a pattern template you define for a utility.
            - It uses character such as (.*) for multiple character, (.) for one character.
            - [] to represent a range of character, or multiple character.
            - (^) to find text file records that begin with particular characters.
            - Text file records where particular characters are at the record's end, append ($)
        
        # Extended Regular Expressions(ERE)
        - (|) allows you to sepcify two possible words or character sets to match.

# Formatting text
    