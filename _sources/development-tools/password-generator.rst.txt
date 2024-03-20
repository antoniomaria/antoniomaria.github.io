===================================
Generate secure and random password
===================================

Sometimes you need to figure some password which fulfils security requirements like:

* Must not contain the user's account name or parts of the user's full name that exceed two consecutive characters
* Must not be one of your last 24 passwords
* Contain characters from three of the following four categories:
* English uppercase characters (A through Z)
* English lowercase characters (a through z)
* Base 10 digits (0 through 9)
* Non-alphabetic characters (for example, !, $, #, %)

You can hit the keyboard randomly and get pseudo random password, but also the utility `pwgen` comes in handy to generate
passwords.

Install pwgen using homebrew
****************************

.. code-block:: console

    brew install pwgen

Secure password
*****************

* -s or --secure.
    Generate completely random passwords
* -B or --ambiguous
	Don't include ambiguous characters in the password

.. code-block:: console

    $ pwgen -Bs 10
      Tv7eqvinNU eoaLcJsyF4 L7wjnVkzsF VjnvcY7pNW WCEb3jdEnV 37zbrpeJbf RrNqKijr47
      NTcs3yVkvL xFqL7yxiJg hCe3F3Hdtr CbjeEN3MHx ChEpYE9jgY A9fVCJotsR 4aNRWUM4Yf

If you need at least one symbol in the password

.. code-block:: console

    $ pwgen -Bsy 10
    $if;_;#4,E `Y3&n=zt); 9mCn\g]^Hs vEzi@3||ws HnJ.?ic3NL LMdYLY9ha$ (>]7ME[Jsj
    4'YK]Hz9:& ;z93{3t(Cd |Yh9V'Utk% *hPtTvnX4V 79${^`+K~M 473w?XyTv| n\;jx"Y!3_

When you are clear with security requirements you can add it in .bash_profile and call it from the shell.
Another alternative is to use bash aliases.

.. code-block:: bash

   genpasswd() { pwgen -Bs $1 1 |pbcopy |pbpaste; echo “Has been copied to clipboard” }


Interesting links
*****************

* `<https://formulae.brew.sh/formula/pwgen>`_