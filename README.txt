
                          Tournament: Swiss Pairings

  What is it?
  -----------

  This is the second project in Udacity's Fullstack Nanodegree Program. The
  main module, tournament.py, holds a series of functions that perform various
  tasks on a postgresql database. This module contains all the functions needed
  to host and run a tournament, including create, modify, and delete the
  members, players in a tourney, or match records. Most important is the
  swiss-pairing function, which ensures the players are paired fairly and
  relatively evenly throughout a tournament and that no players match more than
  once or have two rounds with a 'bye'.
  Future plans: Complexity is quadratic. If some way to call all possible pairs
  from database at one time, the run time for large data sets would be greatly
  reduced. As of now, all test pass with data sets of ____ in ____ ms:
  18: 2791
  36: 4844
  72: 9949
  144: 8573
  288: 145,975

  How does it work?
  ------------------

  The pairing algorithm, swissPairing(), relies on a couple other functions to
  run; remainingOpponents() and recursivePairFinder().
  --swissPairings: checks to see if tourney is in progress, adds a 'BYE' if
  player count is odd, and runs either initial pairing or subsequent pairing
  functions based on whether tournament is in progress.
  The initial pairings splits the players in half and pairs each with the
  adjacent player; for 6 players, ordered from highest seeded to lowest, this
  would result in a table of [A,B,C,D,E,F] being paired as [(A,D),(B,E),(C,F)].
  This ensures strong players are not put against each other in the first round,
  and makes sure the stronger players have higher opponent match wins where
  there are ties.
  The subsequent pairing runs a set of players, ordered by wins, then seedings,
  through the recursivePairFinder.
  --recursivePairFinder: continuously removes a successful pair every time it
  goes a level deeper. When the list of players is emptied, each pair that was
  removed is added to the pair_list on the way back up. The list of possible
  pairs is generated by the remainingOpponents function.
  --remainingOpponents: queries the players and matches tables to find opponents
  that the currently selected player, passed in from recursivePairFinder, has
  not yet played against. These are ordered by the difference between the
  player's and opponent's scores, and then by the seed score (ascending). This
  is done to ensure that players are put against their most even matches towards
  the end of the tournament.


  Documentation
  -------------

  To run a tournament, follow the 'Installation' section below, then populate
  the members table with players as they sign up with registerMember(name). When
  it is time to start a tournament, add the members that are participating in
  the tourney with registerPlayer(member ID). After all players are registered
  in the players table, run swissPairings(tourney id). When the matches have
  completed, record the data with reportMatches(touney id, round, winner id,
  loser id, [optional: isDraw=True,False]). When tourney is complete, run
  endTourney(); this will add tourney data to members' permanent records and
  clear the players table.
    tournament/
    |-- README.txt
    |-- test.py
    |-- tournament.py
    |-- tournament.sql

  Installation
  ------------

  Run `psql -f tournament.sql` to create the database and tables. Ignore the
  errors that say database and tables do not exist the first time this is ran;
  these are just an attempt to drop any existing database and tables from
  previous sessions.



  Contacts
  --------

     o Contact me at school.kde@gmail.com or have a look at my current tinkering
       at shtav.com