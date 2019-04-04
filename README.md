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
