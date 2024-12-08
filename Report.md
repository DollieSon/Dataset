## General Report

We used the Steam games Dataset with over 90,000 rows, specifically we used the apriori algorithm on 3 columns, the genre, tags, and categories
We used an external library called mlxtend because there was no apriori algorithm in numpy and pandas (that we know of).
Because every column had a lot of unique values we had to change the minimum support to a very small number (0.05) instead of 0.5
Due to the nature of the apriori algorithm describing things that occur often together, it rarely leads to interesting relationships but instead braindead-obvious ones. This is also the reason why we had to reduce the minimum support

To differentiate categories,tags and genre is a very confusing thing to do as they are often used interchangeably.

Categories - A general label set by steam to organize and group tags
Tags - Steam allows games to have user-defined tags, initially a game's tags are equal to it's genre but overtime the most popular user-defined tags will become it's tags
Genre - These are labels that are set by the developers

Categories -> Tags -> Genre

## Genre

(show the number of unique genre)
(show the most common genres)

this column is by far the least varied column as every game has mostly 1 genre

The one with the highest confidence is
"Casual","Action" -> "Indie"
with a confidence of 0.844 and a lift of 1.211 and a leverage of 0.195
but the most interesting fact about this column is the "indie" genre, with most of the relationships that had a high confidence having a consequent of "indie"
this says that the indie genre is not only common but is also varied, it could also be because of how easy it is to be called an "Indie" game

## Categories Report

(show the number of unique categories)
(show the common number of categories)

this column is the column that least describes the game itself but it's features, such as In-App Purchases, Trading Cards, Online Co-Op. Because categories mostly have more than 4 labels, but does not have enough unique labels, this causes some calculated values to be very high

The interesting relationships that we found are:
antecedent -> consequents
"Online PvP", "PvP" and "Single-Player" -> "Multi-Player"

- this had the biggest confidence that we had with 1.0 however it had a lift of 5.320 and a leverage of 0.043, which is still high but it does raise alarm that the high confidence might have been because if the popularity of Y (Multiplayer) which is the common drawback of measuring confidence.
- This is supported by the large amount of \_**\_XX\_\_**
- It also very interesting that in the antecedent is "Single-Player"
  though this is somewhat diffrent from
  "PVP" -> "Multi-player"
- this had also a large confidence with 0.998 with a lift of 5.31 but had a leverage of 0.096, with it being one of the highest relationship in terms of leverage
- which makes sense as a Player-Versus-Player game would require multiple players playing.

in general, the categories column had the highest lift out of the three (Categories/Tags/Genre)
One of the highest lift was
'Single-player', 'Remote Play Together', 'Multi-player' <-> 'Shared/Split Screen'
with a lift of 12.7675
'Multi-player', 'Remote Play Together' <->'Shared/Split Screen'  
with a lift of 12.7664

also note that lift symmetrical and does not calculate directional relationship

This means that when there is a high association factor in Multi-Player and Remote Play Together and "Shared/Split Screen". This could be because of there are a lot of Multiplayer games which can easily impliment Shared/Split Screen as well as Steam's Remote Play Feature that allows a player to host a game and allow other user to join from any device

The interesting thing about is that it does not specify what kind of multi-player game it is whether it is "Co-op" or "PVP". Those two opposite playstyles might have been the reason why both are not in the sets with high lift

## Tags Report

(show the number of unique tags)
(show the most common tags)
(show weird/interesting tags)

tags has the most amount of unique tags, this is due to the nature of how steam creates tags. a user can create a his own tag but once a lot of users tag a game with the same tag, that tag becomes permanent onto the game.

of the top 10 highest confidence, 4 consequents were "Action" as we well as a lot of "Singleplayer" consequents with most of its antecedents having "Indie"
this could have a lot meanings, perhaps "Singleplayer" is just compatible with almost all games, or perhaps Most indie games are singleplayer games in one way or another
weirdly, "FPS" -> "Action" was one of the highest but "FPS" -> "Shooter" was not
there were obvious ones as well, such as "2D platformers" -> "2D", "Action-Adventure","Action" -> "Adventure",

the most common relationship are between "Indie","Singleplayer","Pixel Graphics","2D", these 4 always seem to corelate to one another.

though the relationship "3D" <-> "First Person" with a lift of 2.8

## Overall Report

though this data showed some trend, there might be some possibility that it was skewed due to the frequency of some items.

the three columns had very interesting variations that caused weird calculations

Genre: Low Amount of Labels, Low Amount of Variety. "Indie" became dominant/common
Categories: Large Amount of Labels, Low Amount of Variety. "Multiplayer" became dominant/common
Tags: Large Amount of Labels, Large Amount of Variety. "Indie" became dominant/common

We also realized the largest drawback of the apriori algorithm, which was computation power, due to the large number of rows we had to adjust and lower our minimum support threshold which in turn required a lot of extra computation power
