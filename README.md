# MakeTea
Short program that works out volumes for a specific container.

This is based on the assumption that the average cup of tea has
300ml water, 15ml milk, 1 teaspoon sugar (equivilant to 4g) and 1 teabag


This calculates the volume of the cylinder

> cylinderVol :: Float -> Float -> Float
> cylinderVol r h = r^2 * pi * h


These set the types for mug and ml so that I don't have to keep writing out
loads of Floats

> type Mug = (Float, Float)
> type Ml = Float


Each of these is a function which works out the amount of contents for each
component of tea

> water :: Mug -> Ml
> water (r, h) = (cylinderVol r (0.9*h)) * (300/319)

> milk ::  Mug -> Ml
> milk (r, h)= (cylinderVol r h * (15/319))

> sugar :: Mug -> Int
> sugar (r, h)= floor(cylinderVol r h * (1/319))

> teabags :: Mug -> Int
> teabags (r, h)
>    | (sugar (r, h) == 0) = 1
>    | otherwise           = (sugar (r, h))


This converts the radius and height into a list for each compnent

> tea :: Mug -> (Ml, Ml, Int, Int)
> tea (r, h) = (water (r, h), milk (r, h), sugar (r, h), teabags (r,h))

> output :: (Ml, Ml, Int, Int) -> String
> output (w, m, s, t) = "Water (ml): " ++ show w ++
>                       "\nMilk (ml): " ++ show m ++
>                       "\nTeaspoons of Sugar: " ++ show s ++
>                       "\nTeabags: " ++ show t



This outputs the result in a format which is easy to read

> makeTea :: Mug -> IO ()
> makeTea (r, h) = putStrLn (output (tea (r, h)))
