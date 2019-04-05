# scss


$small : 320px;
$medium: 576px;
$large: 720px;


@function fluid-type($properties, $min-vw, $max-vw, $min-value , $max-value) {
  @each $property in $properties {  
    $max-value: 50px;
   @return  calc(#{$min-value} + #{($max-value - $min-value)} * (100vw - #{$min-vw}) / #{($max-vw - $min-vw)});
   
  }
}

@mixin bp($point, $property) {
    @if $point == papa-bear {
      @media (max-width: 1600px) { 
        $min-v: 200px;
        #{$property}:fluid-type($property,$min-v ,576px ,30px ,40px );
        @content;
      }
    }
    @else if $point == mama-bear {
      @media (max-width: 1250px) { @content; }
    }
    @else if $point == baby-bear {
      @media (max-width: 600px)  { 
        
        @content; }
    }
  }

h1 {
    font-size: 15px;
    @include bp(papa-bear, padding, ) {
        background-color: aqua;
    }
}
////////////////////////////////////////////////////////



@import "mixins";

$IncProp:(padding, margin);
$DecProp:(font-size);

*{
    margin: 0;
    padding: 0;
}

html,body {
    vertical-align: baseline;
    box-sizing: border-box;
    font-family: 'Poppins';
    font-size: $base-value;
    text-align: center;

}

body {
    background-color: #CCFBFE;
}


.main-container {
    width: 100%;
    height: auto;
    display: flex;
    flex-direction: row;
    padding-top: 15px;

    .col {
        // @include CommonMP();
        @include coolcal($IncProp);
        a {
            text-decoration: none;
            color: black;
        }
    }

    .col-2 {
        $width : 20%;
        width: $width;
        //  @include calfont-size($width);
         @include calfont-size($width);
        background-color: #CDACA1;
    }
    .col-3 {
        $width : 30%;
        width: $width;
         @include calfont-size($width);
        background-color: #CD8987;
    }
    .col-5 {
        $width : 50%;
        width: $width;
         @include calfont-size($width);
        background-color: #B5D6B2;
    }

    @media (min-width: 320px) {
        .col-2 {
            $width : 30%;
            width: $width;
            @include calfont-size($width);
            
        }
        .col-3 {
            $width : 30%;
            width: $width;
            @include calfont-size($width);
           
        }
        .col-5 {
            $width : 30%;
            width: $width;
            @include calfont-size($width);
        }
    }

    @media (min-width: 800px) {
        .col-2 {
            $width : 25%;
            width: $width;
            @include calfont-size($width);
        }
        .col-3 {
            $width : 25%;
            width: $width;
            @include calfont-size($width);
        }
        .col-5 {
            $width : 50%;
            width: $width;
            @include calfont-size($width);
        }
    }

    @media (min-width: 1024px) {
        .col-2 {
            $width : 20%;
            width: $width;
            @include calfont-size($width);
        }
        .col-3 {
            $width : 30%;
            width: $width;
             @include calfont-size($width);
        }
        .col-5 {
            $width : 50%;
            width: $width;
            @include calfont-size($width);
        }
    }
}



h1 {
    font-size: 15px;
    background-color: aqua;
    // @include bp(sm-wn,$IncProp);
    @include coolcal($IncProp);

    @include bp(sm-wn, $DecProp) {
        z-index: 1;
    }
    @include bp(md-wn, $DecProp) {
        z-index: 2;
    }
    @include bp(lg-wn, $DecProp) {
        z-index: 3;
    }
}


////////////////////////////////////////////////////////


$base-value: 1.2vw;

@mixin CommonMP {
    margin: 15px;
    padding: 15px;
}
                                                        
@function vw($value) {
    @return calc(#{$base-value} * #{$value});
}

@mixin coolcal($properties) {
    @each $property in $properties {
        @if $property=='margin' {
            #{$property}: vw(1.75);   
        }
        @else if $property=='padding' {
            #{$property}: vw(1.25);  
        }
    }
}


@mixin coolcalfl($properties) {
    #{$properties}: vw(1.25); // 18     
}
@mixin coolcalfm($properties) {
    #{$properties}: vw(1.125);     
}
@mixin coolcalfs($properties) {
    #{$properties}: vw(1);        
}




@mixin bp($point, $property) {
    @if $point==sm-wn {
        @media (min-width: 320px) {
            @if $property=='font-size' {
                @include coolcalfl($property);
            }
            @else {
                @include coolcal($property);
            }
            @content;
        }
    }

    @else if $point==md-wn {
        @media (min-width: 800px) {
            @if $property=='font-size' {
                @include coolcalfm($property);
            }
            @else {
                @include coolcal($property);
            }
            @content;
        }
    }

    @else if $point==lg-wn {
        @media (min-width: 1024px) {
            @if $property=='font-size' {
                @include coolcalfs($property);
            }
            @else {
                @include coolcal($property);
            }
            @content;
        }
    }
}


@mixin  calfont-size($ratio) {
    @if $ratio <= 20% {
        @include coolcalfs(font-size);
    } @else if $ratio <= 30% {
        @include coolcalfm(font-size);
    } @else if $ratio >= 50% {
        @include coolcalfl(font-size);
    }
}


////////////


<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Adjust font acc to parent height</title>
    <link rel="stylesheet" href="main.css">
    <link href="https://fonts.googleapis.com/css?family=Poppins" rel="stylesheet">
</head>

<body>
    <h1>Adjusting TypoGraphy as per the parent / outer width: height</h1>
    <div class="main-container">
        <div class="col col-2">
            <a href="#">Link for small container</a>
        </div>
        <div class="col col-3">
            <a href="#">Link for medium container</a>
        </div>
        <div class="col col-5">
            <a href="#">Link for large container</a>
        </div>
    </div>
</body>

</html>
