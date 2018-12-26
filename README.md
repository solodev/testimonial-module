# testimonial-module

## Prerequisites
<ul>
	<li><a target="_blank" href="https://getbootstrap.com/">Boostrap4</a></li>
	<li><a target="_blank" href="https://fontawesome.com/">FontAwesome5</a></li>
	<li><a target="_blank" href="https://cloud.google.com/maps-platform/">Google Maps</a></li>
</ul>

## Step 1: Add the Form
 - testimonial-form.tpl

Create a calendar for the Testimonials and upload the following form.

```
<div class="panel-group">
  <div class="panel panel-default">
    <div class="panel-heading">
      <h4 class="panel-title"><a aria-expanded="true" data-toggle="collapse" href="#collapseStatus">Post Status<span
            class="toggle" aria-hidden="true"></span></a></h4>
    </div>

    <div class="panel-collapse collapse in" id="collapseStatus">
      <div class="panel-body">
        <div class="row">
          <div class="col-md-6">
            <h2><label class="label-control" for="post_status">Post Status</label></h2>
            <select class="form-control" name="post_status" type="text">
              <option value="Draft">Draft</option>
              <option value="Published">Published</option>
            </select>
          </div>

          <div class="col-md-6">
            <h2><label class="label-control" for="post_featured">Featured</label></h2>

            <p class="subText">If set to "Yes", the Quick Link will be featured in the top navigation and homepage.</p>
            <select class="form-control" name="post_featured" type="text">
              <option value="Yes">Yes</option>
              <option value="No">No</option>
            </select>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="panel-group">
  <div class="panel panel-default">
    <div class="panel-heading">
      <h4 class="panel-title"><a aria-expanded="true" data-toggle="collapse" href="#collapseQuick">Quicklink Details<span
            class="toggle" aria-hidden="true"></span></a></h4>
    </div>

    <div class="panel-collapse collapse in" id="collapseQuick">
      <div class="panel-body">
        <div class="row">
          <div class="col-md-6">
            <h2><label class="label-control" for="quick_title">Quicklink Title</label></h2>

            <p class="subText">The publicly viewable title.</p>
            <input class="form-control" id="quick_title" name="quick_title" type="text" />
          </div>

          <div class="col-md-6">
            <h2><label class="label-control" for="quick_ref">Quicklink Link</label></h2>

            <p class="subText">The link URL (use relative links for internal links).</p>
            <input class="form-control" id="quick_ref" name="quick_ref" type="text" />
          </div>
        </div>
        <div class="row">
          <div class="col-md-6">
            <h2><label class="label-control" for="quick_external">Quicklink External</label></h2>

            <p class="subText">Does the link go to some web page off of the site?</p>
            <select class="form-control" id="quick_external" name="quick_external" type="text">
              <option value="Yes">Yes</option>
              <option value="No">No</option>
            </select>
          </div>

        
        </div>
      </div>
    </div>
  </div>
</div>


<div class="panel-group">
  <div class="panel panel-default">
    <div class="panel-heading">
      <h4 class="panel-title"><a data-toggle="collapse" href="#collapseAdvanced">Advanced <span class="toggle"
            aria-hidden="true"></span></a></h4>
    </div>

    <div class="panel-collapse collapse" id="collapseAdvanced">
      <div class="panel-body">
        <div class="row">
          <div class="col-md-12">
            <h2><label class="label-control" for="post_javascript">Custom JavaScript</label></h2>

            <p class="subText">(Optional) Use the following textbox to embed any custom JavaScript including tracking
              pixels and Google Analytics scripts. Be sure to open your JavaScript with a &lt;script&gt; tag and close
              everything with a &lt;/script&gt; tag.</p>
            <textarea class="form-control" id="post_javascript" name="post_javascript"></textarea>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<script>
  $('.wysiwyg').ckeditor(function () {}, {
    customConfig: '/CK/config.js',
    height: '600px',
    basePath: '/CK/',
    toolbar: 'WP'
  });
</script>

```

## Step 2: Add the Repeater
 - testimonial-repeater.tpl

Add the following repeater shortcode wherever you want the testimonial slider

```
<section class="position-relative">
  <div class="slick slick-testimonials w-100" style="background: url('/_/images/testimonials1.jpg') center/cover no-repeat;">
  [repeater id="13" limit="0,3" order="start_time desc" display_type="news" where="post_status='Published'"]
    <div class="slide position-relative text-white text-center">
      <div class="container h-350p h-md-450p d-flex flex-column justify-content-center">
        <div class="font-weight-bold w-lg-600p mx-auto">
          <span class="font-italic lead">{{testimonial_content}}</span>
          <p class="lead mt-4 mb-0">{{testimonial_author}}</p>
        </div>
        <p class="text-uppercase small">{{testimonial_author_title}}</p>
      </div>
    </div>
  [/repeater]
  </div>
</section>
```


## Step 4: Add the SCSS/CSS
 - /_/scss/slider.scss
 
 ```
 @import "../mixins";

.slick {
  line-height: 0;
  .slick-list {
    .slick-track {
      // Fix for sliders that have slides with different heights
      display: flex;
      align-items: center;
      .slide {
        line-height: 1.5;
        @include media-breakpoint-up(md) {
          &.slide-img-right {
            img {
              max-width: 360px;
            }
          }
        }
        .slide-content {
          width: 100%;
          @include media-breakpoint-up(lg) {
            max-width: 40%;
          }
          @include media-breakpoint-up(xl) {
            max-width: 25%;
          }
        }
      }
    }
  }
  .slick-dots {
    text-align: center;
    position: absolute;
    bottom: 30px;
    left: 0;
    right: 0;
    padding: 0;
    margin: 0;
    @include media-breakpoint-up(sm){
      bottom: 15px;
    }
    li {
      position: relative;
      display: inline-block;
      width: 20px;
      height: 20px;
      padding: 0;
      cursor: pointer;
      border-bottom: 0;
      margin: 0;
      button {
        font-size: 0;
        line-height: 0;
        display: block;
        padding: 5px;
        cursor: pointer;
        border: 0;
        outline: none;
        background: transparent;
        &:before {
          content: '\f111';
          font-family: $fa-font;
          font-size: ($font-size - 0.125rem);
          text-align: center;
          line-height: 1;
        }
      }
      &.slick-active {
        button {
          &:before {
            font-weight: 600;
          }
        }
      }
    }
  }
  &.blog-slider {
    .slick-dots {
      bottom: -26px;
      @include media-breakpoint-down(sm){
        bottom: -60px;
      }
    }
  }
  &.slick-testimonials {
    .slick-dots {
      button {
        &:before {
          color: $white;
        }
      }
      @include media-breakpoint-up(sm){
        bottom: 36px;
      }
    }
  }
}
.carousel-controls {
  width: 100%;
  position: absolute;
  left: 0;
  z-index: 1;
  top: calc(100% - 100px);
  @include media-breakpoint-up(md) {
    top: calc(50% - 25px);
  }
  .prev,
  .next {
    position: absolute;
    top: 0;
    color: $white;
    cursor: pointer;
    width: 40px;
    height: 100px;
    @include media-breakpoint-up(md) {
      width: 60px;
    }
    &:before,
    &:after {
      content: "";
      position: absolute;
      height: 2px;
      width: 100%;
      background: $white;
      transition: transform .25s ease, bottom .25s ease;
    }
  }
  .prev {
    left: 0;
    &:before {
      @include transform(rotate(-60deg));
    }
    &:after {
      @include transform(rotate(60deg));
      bottom: 64px;
      @include media-breakpoint-up(md) {
        bottom: 47px;
      }
    }
    @include media-breakpoint-up(md) {
      &:hover {
        &:before {
          @include transform(rotate(-45deg));
        }
        &:after {
          @include transform(rotate(45deg));
          bottom: 55px;
        }
      }
    }
  }
  .next {
    right: 0;
    &:before {
      @include transform(rotate(60deg));
    }
    &:after {
      @include transform(rotate(-60deg));
      bottom: 64px;
      @include media-breakpoint-up(md) {
        bottom: 47px;
      }
    }
    @include media-breakpoint-up(md) {
      &:hover {
        &:before {
          @include transform(rotate(45deg));
        }
        &:after {
          @include transform(rotate(-45deg));
          bottom: 55px;
        }
      }
    }
  }
}

 ```
## Step 4: Add the JS
 - /_/js/slider.js
 
 ```
 
 $(document).ready(function () {
  $('.slick').slick({
    lazyLoad: 'ondemand',
    slidesToShow: 1,
    autoplay: 0,
    dots: true,
    arrows: false
  });
});

 ```
