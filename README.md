## Installation

Since this program is written in the Python programming language, it is necessary to have Python installed on your system.

Run the following command to verify the installation:
python --version

If you do not have any version installed, visit the following site to download it:
https://www.python.org/downloads/

To install the necessary library for generating a PDF file:

pip install reportlab

This library allows generating a PDF file which displays the similarity percentage between the source codes in a readable format.
Execution Instructions

To run the code using the "diff" method, use the following command:

python ./diffutLinks/main.py ./dataset/your_source_code_name_1 ./dataset/your_source_code_name_2

To run the code using the “suffixArray” method, use the following command:

python ./suffixArray/main.py ./dataset/your_source_code_name_1 ./dataset/your_source_code_name_2

To run either of the two commands above with preprocessing, which renames non-reserved keywords to a default name, removes spaces and comments, you need to add the following flag:

--preprocess

Preprocessing

The preprocessing file cleans the source code by removing comments (both single-line and multi-line) and unnecessary spaces. It also replaces all non-reserved variable and function names with generic identifiers (like id1, id2, etc.), which helps avoid differences caused only by name changes. It uses the tokenize module to analyze and convert the code into tokens, then reconstructs the code without comments and with standardized names, returning the result as a single-line string. The main goal is to normalize the code, ensuring only logical differences are considered during the comparison.
Execution Flow
DiffString Method

This method calculates similarity based on a string difference (diffString). It determines how many characters are identical between the files and then calculates a similarity percentage based on the length of the shorter file.

Steps:

    Preprocessing (optional):

        If the --preprocess flag is used, a function is called to normalize the test files as described above.

    DiffString Preparation:

        Converts the diffString into a list of lines (diffList) by splitting at line breaks.

    Iterating Through Differences:

        Each line (except the last one) is compared with the next one to find changes.

    Change Identification:

        Lines starting with - indicate a deletion (for the left file).

        Lines starting with + indicate an addition (for the right file).

        Lines starting with ? mark changed characters in a line.

    Counting Differences:

        Counts the number of different characters. If the character is not a space, it increases the totalCharEqualities counter.

    Similarity Calculation:

        The similarity percentage is calculated with:

        Similarity (%) = ((length of the shorter file - differences) / length of the shorter file) × 100

        Rounded to two decimal places.

Suffix Array Method

This method is based on finding and comparing suffixes of the texts. The number and length of common suffixes indicate the similarity between the texts. The more and longer common suffixes, the greater the similarity.

Steps:

    Preprocessing (optional):

        As above, used if the --preprocess flag is included.

    Suffix Array Construction:

        Combines both texts (text1 and text2) with special characters (# and $) and creates a suffix array (alphabetically sorted suffixes).

    Finding Longest Common Suffixes:

        Iterates through the suffixes of the combined string.

        Compares consecutive suffixes from different texts and calculates their longest common suffix using commonSuffixLen.

        Stores any found common suffixes in a list.

    Removing Nested Suffixes:

        Filters out suffixes that are completely contained within longer ones to avoid double counting.

        Only the most significant, non-nested suffixes are kept.

    Result:

        The final result is a list of the longest common suffixes between the two texts, representing their similarity areas.

        Overall similarity could later be calculated by evaluating how many common suffixes exist and their lengths.

Libraries Used

    difflib
    Used to compare character sequences to determine similarity percentage.

    tokenize
    Used to break Python source code into tokens such as keywords, variable names, operators, etc.

    token
    Works with tokenize to define constants for various token types like NAME, NUMBER, STRING, OP, etc.

    io
    Creates an in-memory binary file-like object to simulate file operations without writing to disk.

    argparse
    Creates a command-line interface to receive and manage arguments, allowing the user to alter execution flow.

    reportlab
    Generates a PDF file with the similarity checking results for easier reading.

To install:

pip install reportlab